# EiffelActivityTriggeredEvent
The EiffelActivityTriggeredEvent declares that a certain activity - typically a build, test or analysis activity - has been triggered by some factor. Note that this is crucially different from the activity execution having _started_ (as declared by [EiffelActivityStartedEvent](./EiffelActivityStartedEvent.md)).

In a situation where execution follows immediately upon triggering these two events should be sent together. Where that is not the case (e.g. due to queuing) the time delta between EiffelActivityTriggeredEvent and EiffelActivityStartedEvent constitutes the queue time.

## Data Members
### data.name
__Type:__ String  
__Required:__ Yes  
__Description:__ The name of the activity. Uniqueness is not required or checked, but is useful.

### data.category
__Type:__ String  
__Required:__ No  
__Description:__ The category of the activity. This can be used to group multiple similar activities for analysis and visualization purposes. Example usage is to label the similar but unique build activities of all the components of system X as "System X Component Build" (whereas the name would be e.g. "System X Component Y Build").

### data.triggers
__Type:__ Object[]  
__Required:__ No  
__Description:__ The circumstances triggering the activity.

#### data.triggers.type
__Type:__ String  
__Required:__ Yes  
__Legal values:__ MANUAL, EIFFEL_EVENT, SOURCE_CHANGE, TIMER, OTHER  
__Description:__ The type of trigger.  
MANUAL signifies that the activity was manually triggered.  
EIFFEL_EVENT signifies that the activity was triggered by one or more Eiffel events. These events should be represented via __CAUSE__ links.  
SOURCE_CHANGE signifies that the activity was triggered as a consequence of a detected source change __not__ represented by Eiffel events.  
TIMER signifies that the activity was triggered by a timer.  
OTHER signifies any other triggering cause.

#### data.triggers.description
__Type:__ String  
__Required:__ No  
__Description:__ A description of the trigger.

### data.executionType
__Type:__ String  
__Required:__ No  
__Legal values:__ MANUAL, SEMI_AUTOMATED, AUTOMATED, OTHER  
__Description:__ The type of execution (often related to, but ultimately separate from, __data.trigger.type__).

## Examples
* [Simple example](https://github.com/Ericsson/eiffel-examples/blob/master/events/EiffelActivityTriggeredEvent/simple.json)