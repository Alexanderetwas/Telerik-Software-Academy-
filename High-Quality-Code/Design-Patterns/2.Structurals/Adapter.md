# Structural Patterns

## Adapter/�������

 * ����������� ���������� �� ����� ����, ���� �� �� ���� �� ���� ��������� �� �������.
 * ��������� �� ������� � ������������ ���������� �� ������� ������.
 	
������������ �� ������� �� ������ ��� ��������� �� ������������ ����������. �������� ���� �� ������ ����� �����, �� �� ����, ������ ����������, ����� ����� �� ������� �������� �� ������� �� � ������� � ����, ����� ������ ������ �� ��������. � ���������� �� ���������� �� ��������, �������� � ������� ��� wrapper � translator.

## ���� ��������:

![Factory method](http://www.dofactory.com/images/diagrams/net/adapter.gif)

����������:

 * *__Target:__* �������� ����������� ���������, ����� �������� ��������.
 * *__Adapter:__* ������������ ���������� *Adaptee* ��� ���������� *Target*.
 * *__Adaptee:__* �������� ����������� ���������, ����� �� ������ �� ����������.
 * *__Client:__* ������ � ������, ����������� �� �� ���������� *Target*.

�������� ���:

```
using System;
 
namespace Adapter
{
  class MainApp
  {
    static void Main()
    {
      // Create adapter and place a request
      Target target = new Adapter();
      target.Request();
 
      // Wait for user
      Console.ReadKey();
    }
  }
 
  class Target
  {
    public virtual void Request()
    {
      Console.WriteLine("Called Target Request()");
    }
  }
 
  class Adapter : Target
  {
    private Adaptee _adaptee = new Adaptee();
 
    public override void Request()
    {
      // Possibly do some other work
      //  and then call SpecificRequest
      _adaptee.SpecificRequest();
    }
  }

  class Adaptee
  {
    public void SpecificRequest()
    {
      Console.WriteLine("Called SpecificRequest()");
    }
  }
}
```