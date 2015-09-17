# Structural Patterns

## Composite/����������

 * ��������� ������������� �� �������� �� ��� ������ � ���������� ���������
 * ���� ���������� ������������ ������ ��� ����� �� ������ �� ����� ��������� �������

�������� ���������� ��������� �� ���� ��������� ���������� ���������, ����� ������� �� ����� ���� �� ���� ������� �� ������� ������ ������. ������� ������ � ���������������� ����� �� ������ ��������, � ����� �������������� �������� � �� �����, ��� ���� ��� �������� ���� �� ����������, � ���-������ �� ������������ ���������. ������������ ��������� ����� ������� �� �������� �� ���� �� ������� ������ ��������.

## ���� ��������:

![Factory method](http://www.devlake.com/design-patterns/composite/composite1.png)

����������:

 * *__IComponent:__* ���� ��������� ��� ���������� ���� �������� ��������, ����� ������ �� ���������� ����� *Leaf*, ���� � *Composite* ���������. ������� *Operation()* � ��� � ���� �� ���� ������������� �� ������ �������� � �������.
 * *__Leaf:__* ���������� �� ���� ��� �� ����� �� ���� ����� �������� ��� ���� �� �������� ���������� ������������� �� ����� *Operation()* �����.
 * *__Composite:__* ���������� �� ���� ��� ����� �� ���� 0 ��� ������ �������� ��� ���� ��. ��������, ����� �������� �� ��������:
 	* *__AddComponent:__* ������ ��� ������� ��� �������
 	* *__GetChild:__* ����� ������ �������� ��� ������� 
 	* *__Operation:__* ����������� ������������� �� ����� �� ������ �������� �����
 	* *__RemoveComponent:__* �������� ������� �� ����, ����� �� ��� �������
 

�������� ���:

```
class Program
{
    static void Main()
    {
        Worker worker = new Worker("Worker Pesho", 500);
        Manager firstManager = new Manager("Boss Gosho", 200);
        Manager secondManager = new Manager("Boss Bai Ivan", 5);
        Manager thirdManager = new Manager("Kaka Mara", 120);
        Worker secondWorker = new Worker("Worker Gruyo", 600);

        //set up the relationships
        firstManager.AddSubordinate(worker); //Pesho works for Gosho
        secondManager.AddSubordinate(firstManager); //Gosho works for Bai Ivan
        secondManager.AddSubordinate(thirdManager); //Kaka Mara works for Bai Ivan
        thirdManager.AddSubordinate(secondWorker); //Gruyo works for Kaka Mara

        //Bai Ivan writes some code and asks everyone else to do the same
        if (secondManager is IEmployee)
        {
        	(secondManager as IEmployee).WriteSomeCode();
        }
    }
}

public interface IEmployee
{
    void WriteSomeCode();
}

public class Worker : IEmployee
{
    private string name;
    private int linesOfCodeWritten;

    public Worker(string name, int linesOfCodeWritten)
    {
        this.name = name;
        this.linesOfCodeWritten = linesOfCodeWritten;
    }

    void IEmployee.WriteSomeCode()
    {
        Console.WriteLine(name + " wrote " + linesOfCodeWritten + " lines of code.");
    }
}

public class Manager : IEmployee
{
    private string name;
    private int linesOfCodeWritten;

    private List<IEmployee> subordinate = new List<IEmployee>();

    public Manager(string name, int linesOfCodeWritten)
    {
        this.name = name;
        this.linesOfCodeWritten = linesOfCodeWritten;
    }

    void IEmployee.WriteSomeCode()
    {
        Console.WriteLine(name + " wrote " + linesOfCodeWritten + " lines of code.");
        //show all the subordinate's lines of code
        foreach (IEmployee i in subordinate)
            i.WriteSomeCode();
    }

    public void AddSubordinate(IEmployee employee)
    {
        subordinate.Add(employee);
    }
}
```