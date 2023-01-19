# JHA Technical documents in markdown?

```C#
  public enum AchImportFormatType
    {
        None = 0,
        
        [Description("CSV")]
        Csv,
        
        [Description("Fixed")]
        Fixed,
        
        [Description("Tab")]
        TabDelimited,
        
        [Description("Space")]
        SpaceDelimited,
        
        [Description("Binary")]
        Binary,
        
        [Description("NACHA")]
        NACHA
    }
```

##### Sequence Diagram for the controller GET operation

```mermaid
sequenceDiagram
    actor Caller as Banno
    participant Int as Interceptors
    participant C as GetAchImportFormatController
    participant A as GetAchImportFormatAction
    Caller ->> Int : GetAchImportFormatRequest
    break when invalid input is received
        Int --> Caller : Return GetAchImportFormatResponse (failure) 
    end
    Int ->> C : GetAchImportFormatRequest
    C ->> A : GetAchImportFormatRequest
    break when error occurs or success = false
        A ->> C : Return GetAchImportFormatResponse (failure) 
        C ->> Caller : Return GetAchImportFormatResponse (failure) 
    end
    C ->> Caller : GetAchImportResponse (success)
```
