# swedish-identification-number

The all in one library for swedish identification numbers such as personal (personnummer), coordination (samordningsnummer) and business registration number (organisationsnummer).

## Features

### Personal identification number (personnummer)

```
string strVal = "197607012395";           // Or 7607012395, or 760701-2395 or 19760701-2395

PersonalIdentificationNumber identificationNumber = strVal.ToIdentificationNumber();

bool isValid = identificationNumber.IsValid;

```

### Coordination number (samordningsnummer)

```
string strVal = "6512623306";

PersonalIdentificationNumber identificationNumber = strVal.ToIdentificationNumber();
```

### Business registration number (organisationsnummer)
```
string strVal = "2120000142";             // or 212000-0142

BusinessRegistrationNumber identificationNumber = strVal.ToIdentificationNumber();
```

### Validation attributes
TBD

### Fluid validation
TBD

### Ready for entity framework
E.g. An simple customer entity where a customer can be either an private customer or an business customer.

The property IdentificationNumber can hold any type of identification number implementing the IIdentificationNumber interface. There is no need for any backing field or multiple properties.

```
public class Customer
{
    [Key]
    public Guid Id { get; set; }
    
    public IIdentificationNumber IdentificationNumber { get; set; }
    
    public CustomerType Type { get; set; }
    public string Name { get; set; }
}
```
With value conversion in EF:
```
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder
        .Entity<Customer>()
        .Property(e => e.IdentificationNumber)
        .HasConversion(
            v => v.ToString(),
            v => v.ToIdentificationNumber());
}
```

