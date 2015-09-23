# Behavioral Patterns

## Memento/�������

 * ������� ���������� ��������� �� ������ � ���� ���������� �� ���������� ������� ��� ���������� ���������
 * Undo � save/load ��������

�������� ������� ��������� �� ����� �������� ������ ��������� �� �����, ��� ����� ������� ���� �� ���� ������ ��-�����. �� ����� �� �������� �� ������������, ������������ ���� �� ������ �� ����� ��� �������� ���������, �������� ��������� �������� � ���� ��� undo ����� � �������� �� �������� ���������.

������� �� ���� ������ �, �� ����������� ��� ������ ���� �� ��� ������ �� *Memento* ������, ���� ������ �������������� � ���� �� ������������ ���� ����� *Caretaker*. �������� �� �� ���������� ��� ����� ���������� ��������� �� ���������� ��� �������������.

## ���� ��������:

![Factory method](http://www.devlake.com/design-patterns/memento/memento.PNG)

����������:

 * *__Originator:__* ��������, ����� �� ����� ��������� � ��-����� ��������������:
   * ������������ *state* ������� ����������, �������������� ����������� �� *Originator* ������. ���� � ������������, ����� ��������� � ��������������.
   * ������� *CreateMemento* �� ��������, �� �� �� ������ ����������� �� *Originator*-�. ��� ������� ����� *Memento*, ���������� � ���� ������������ *state* � �� ����� ���� ��������.
   * ������� *SetMemento* ������������ *Originator*-�, ��������� *Memento* �����, ���� �� ��������� � ����� ������������ �� *state*, ����������� ����������� ���������� �� *Memento*, � ����� ������������� � ���� �������� ������ ���������.
 * *__Memento:__* ���� ���� ��������� ������������ �� *Originator*-a � ������������ �� *state*.
 * *__Caretaker:__* ������, ����� ��������� ������� �� *Memento* ������ � ����� ����������� ��� ���� �� �������.
 

�������� ���:

```
public class Program
{
    static void Main()
    {
        Originator<string> orig = new Originator<string>();

        orig.SetState("state0");
        Caretaker<string>.SaveState(orig); //save state of the originator
        orig.ShowState();

        orig.SetState("state1");
        Caretaker<string>.SaveState(orig); //save state of the originator
        orig.ShowState();

        orig.SetState("state2");
        Caretaker<string>.SaveState(orig); //save state of the originator
        orig.ShowState();

        //restore state of the originator
        Caretaker<string>.RestoreState(orig, 0);
        orig.ShowState();  //shows state0
    }
}

//object that stores the historical state
public class Memento<T>
{
    private T state;

    public T GetState()
    {
        return state;
    }

    public void SetState(T state)
    {
        this.state = state;
    }
}

//the object that we want to save and restore, such as a check point in an application
public class Originator<T>
{
    private T state;

    //for saving the state
    public Memento<T> CreateMemento()
    {
        Memento<T> m = new Memento<T>();
        m.SetState(state);
        return m;
    }

    //for restoring the state
    public void SetMemento(Memento<T> m)
    {
        state = m.GetState();
    }

    //change the state of the Originator
    public void SetState(T state)
    {
        this.state = state;
    }

    //show the state of the Originator
    public void ShowState()
    {
        Console.WriteLine(state.ToString());
    }
}

//object for the client to access
public static class Caretaker<T>
{
    //list of states saved
    private static List<memento><T>> mementoList = new List<memento><T>>();

    //save state of the originator
    public static void SaveState(Originator<T> orig)
    {
        mementoList.Add(orig.CreateMemento());
    }

    //restore state of the originator
    public static void RestoreState(Originator<T> orig, int stateNumber)
    {
        orig.SetMemento(mementoList[stateNumber]);
    }
}
```