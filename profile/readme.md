# Coding Standard (WIP)

## Naming
- Names do not use underscores.
- Prefixes always use lower-case letters.
- Access-prefixes are specified first.
- Local variables always begin with a lower-case letter. (Prefixed local variables already follow this rule.) 
- The first letter of every new word in a name is capitalised.

## Prefixes

### Access
- **u** = unsafe
- **i** = private
- **o** = protected

**Note on unsafe functions/variables:**<br>
These must be made private unless exposing them is absolutely necessary.

### Intention/Kind
**Universal**
- **d** = delta (difference)

**float**
- **t** = time (usually float)

**int**
- **f** = frame
- **c** = count
- **n** = number (see note below)
- **x** = index

```C++
dtMeeting = tMeetingEnded - tMeetingStarted;
```

**Note**: Number is not to be confused with count.<br>
Example: When counting frames, the total number of frames would be a count. e.g. `cfRendered`<br>
To specify one of those frames we would use a number. e.g. `nfLastUpdate`<br>
In a sense this is similar to index. However, indices are reserved for accessing containers.

## Braces
Braces that declare a new scope must be on their own line. **Exception:** single-line inline functions.

```C++
//Do this:
void Example()
{
    if (someBool)
    {
        //some code
    }
}

//Permissible:
inline void Example()
{ DoSomething(); };

//NOT this:
void Example() {
    if (someBool) {
        //some code
    } else {
        //some more code
    }
}
```

## Const
For references and pointers use right-to-left const.

```C++
float const& refToSomeFloat
```

Using left-to-right const can help visualise when values are copied.

```C++
const float someFloat
```

## Other

### Validity checks
When checking for validity of passed-in values inside functions,
use an unbraced if-statement with an indented return-statement on the next line,
followed by an empty line, then followed by the remaining code (usually) without declaring an additional scope:

```C++
//Do this:
int Example(bool desiredCondition)
{
    if (!desiredCondition)
        return -1;
		
    //More code goes here:
    // ...
    // ...
}

//NOT this:
int Example(bool desiredCondition)
{
    if (desiredCondition)
    {
        //Two pages of code
    }
    else
    {
        return -1;
    }
}
```
This saves screen-space, turns such checks into an easily recognisable pattern, and adding more lines of code to them is undesired.

**Exception:** After such a check, if the remaining function consists of only one line, use "else".

```C++
//Do this:
void Example(bool desiredCondition)
{
    if (!desiredCondition)
        return;
    else
        DoSomething();
}

//NOT this:
void Example(bool desiredCondition)
{
    if (!desiredCondition)
        return;
		
    DoSomething();
}
```
