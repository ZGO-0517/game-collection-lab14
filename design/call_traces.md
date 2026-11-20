call traces for "contains"

Trace 1: "contains(&[7, 12, 3], 3)"

| Call 3: contains(&[3], 3)                             |
| Receives: values = &[3], target = 3                   |
| Action:   List is not empty. First item 3 == 3.       |
|           Base case reached (found)!                  |
| Returns:  true                                        |

                          | returns true
                          v

| Call 2: contains(&[12, 3], 3)                         |
| Receives: values = &[12, 3], target = 3               |
| Action:   List is not empty. First item 12 != 3.      |
|           Calls contains(&[3], 3) and waits.          |
| Returns:  true (passed up from Call 3)                |

                          | returns true
                          v

| Call 1: contains(&[7, 12, 3], 3)                      |
| Receives: values = &[7, 12, 3], target = 3            |
| Action:   List is not empty. First item 7 != 3.       |
|           Calls contains(&[12, 3], 3) and waits.      |
| Returns:  true (passed up from Call 2)                |


---------------------------------------------------------


Trace 2: "contains(&[7, 12, 3], 5)"

| Call 4: contains(&[], 5)                              |
| Receives: values = &[], target = 5                    |
| Action:   List is empty. Base case reached!           |
| Returns:  false                                       |

                          | returns false
                          v

| Call 3: contains(&[3], 5)                             |
| Receives: values = &[3], target = 5                   |
| Action:   List is not empty. First item 3 != 5.       |
|           Calls contains(&[], 5) and waits.           |
| Returns:  false (passed up from Call 4)               |

                          | returns false
                          v

| Call 2: contains(&[12, 3], 5)                         |
| Receives: values = &[12, 3], target = 5               |
| Action:   List is not empty. First item 12 != 5.      |
|           Calls contains(&[3], 5) and waits.          |
| Returns:  false (passed up from Call 3)               |

                          | returns false
                          v

| Call 1: contains(&[7, 12, 3], 5)                      |
| Receives: values = &[7, 12, 3], target = 5            |
| Action:   List is not empty. First item 7 != 5.       |
|           Calls contains(&[12, 3], 5) and waits.      |
| Returns:  false (passed up from Call 2)               |
