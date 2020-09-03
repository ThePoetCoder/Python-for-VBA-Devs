# Test Worksheet functions

```python
from collections import namedtuple

def test_py_excel_fx(
    sfx_app,
    xl_fxp,
    py_fxp
):
    try:
        xl_fx = getattr(
            sfx_app.WorksheetFunction,   
            xl_fxp.fx
        )
    except AttributeError as e:
        raise AttributeError(
            "You made a typo in the Excel Fx name"
        ) from e
    else:
        xl_result = xl_fx(
            *xl_fxp.kwargs
        )
        py_result = py_fxp.fx(
            *py_fxp.kwargs
        )
    
FxPackage = namedtuple(
    "FxPackage",
    "fx kwargs"
)
```