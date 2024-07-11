```C# 
public abstract class Employee : IPerson
{
    //IPerson
    public string LastName { get; set; }
    public string FirstName { get; set; }


    public DateOnly StartDate { get; set; }

    //virtual property
    public virtual DateTime EndDate { get; set; }

    //abstract property
    public abstract int EmployeeId { get; }

    //derived must implement
    public abstract bool ProcessPayroll();  

    //derived can implement
    public virtual void Terminate(DateTime terminationEffectiveDate)
    {
        Console.WriteLine("Employee terminated");
        EndDate = terminationEffectiveDate;
    }

    //derived can call or hide
    public bool IsActive()
    {
        Console.WriteLine("Employee Active");
        DateOnly current = DateOnly.FromDateTime(DateTime.Now);
        return current > StartDate && DateTime.Now < EndDate;
    }
}
```

- 