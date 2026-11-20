STRIDE cheat sheet

STRIDE-per-element
| Element | type |	S |	T |	R |	I |	D |	E |
| External entity |	✓	|	| ✓ | | | |			
| Process |	✓ |	✓ |	✓ |	✓ |	✓ |	✓ |
| Data flow |	|	✓ |	|	✓ |	✓| |	
| Data store | | ✓ | ? | ✓ | ✓ | |	

| # | Element | Interaction | S | T | R | I | D | E |
|---|---|---|---|---|---|---|---|---|
| 1 | Process | Outbound data flow to a data store | ✓ | | | ✓ | | |
| 2 | Process | Sends output to another process | ✓ | | ✓ | ✓ | ✓ | ✓ |
| 3 | Process | Sends output to an external interactor (code) | ✓ | | ✓ | ✓ | ✓ | |
| 4 | Process | Sends output to an external interactor (human) | | | ✓ | | | |
| 5 | Process | Inbound data flow from a data store | ✓ | ✓ | | | ✓ | ✓ |
| 6 | Process | Inbound data flow from a process | ✓ | | ✓ | | ✓ | ✓ |
| 7 | Process | Inbound data flow from an external interactor | ✓ | | | | ✓ | ✓ |
| 8 | Data flow | Crosses a machine boundary | | ✓ | | ✓ | ✓ | |
| 9 | Data store | Process has outbound data flow to the data store | | ✓ | ✓ | ✓ | ✓ | |
| 10 | Data store | Process has inbound data flow from the data store | | | ✓ | ✓ | ✓ | |
| 11 | External interactor | Passes input to a process | ✓ | | ✓ | ✓ | | |
| 12 | External interactor | Gets input from a process | ✓ | | | | | |
