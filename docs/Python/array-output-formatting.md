## Python 3 (see also):

```
import numpy as np
import sys

a = np.array([0.0, 1.0, 2.0, 3.0])
np.savetxt(sys.stdout.buffer, a)
```
### Python 2:

```
import numpy as np
import sys

a = np.array([0.0, 1.0, 2.0, 3.0])
np.savetxt(sys.stdout, a)
```
## Output:

```
0.000000000000000000e+00
1.000000000000000000e+00
2.000000000000000000e+00
3.000000000000000000e+00
```
### Control the prevision

#### Use fmt:

```
np.savetxt(sys.stdout, a, fmt="%.3f")
````
output:

````
0.000
1.000
2.000
3.000 
````

or:

````
np.savetxt(sys.stdout, a, fmt="%i")
`````

output:

````
0
1
2
3
````

Get a string instead of printing

Python 3:

````
import io
bio = io.BytesIO()
np.savetxt(bio, a)
mystr = bio.getvalue().decode('latin1')
print(mystr, end='')
````

We use latin1 because the docs tell us that it is the default encoding used.

Python 2:

```
import StringIO
sio = StringIO.StringIO()
np.savetxt(sio, a)
mystr = sio.getvalue()
print mystr
```

All in one line

Or if you really want all in one line:

```
a = np.array([0.0, 1.0, 2.0, 3.0])
np.savetxt(sys.stdout, a, newline=' ')
print()
```
Output:
```
0.000000000000000000e+00 1.000000000000000000e+00 2.000000000000000000e+00 3.000000000000000000e+00 
```