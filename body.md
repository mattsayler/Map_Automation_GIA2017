# _Python_ for Mapbook _Automation_

OR

![](./Images/OneMXDtoRule.png)

Matt Sayler
_Clark Public Utilities_

# _Obligatory_ Organization _Stats_ Slide

Public Utility District

Electric and Water Distribution

~200,000 Electric Meters

~400 Employees

# Clark GIS System

ArcGIS 10.2.1

ArcFM 10.2.1c

# Original Mapbook Setup

_~450_ pages of _individually customized_ MXD files

Custom _layouts_ with _selection-set_ layers

Custom _jpegs_ for inset details (_~300_ images)

Custom _'best-fit'_ grid layout for _each_ mapbook

# Example _Old_ System Map

![](./Images/AST4_Original.png)

# Pros:

Highly _specific_ symbology

Covers _edge-case_ maps very well

Fits _user's_ specific _needs_ very well

# Cons:

Management _nightmare_ for GIS Dept.

_Turn-around_ time commonly measured in _days_ per page

_Complex_ process to _add_ new pages

# Problem

_Reduced_ staff resources

# Solution

Standarize map _elements_ and leverage _Data Driven Pages_ functionality

# _What_ are [Data Driven Pages](http://resources.arcgis.com/en/help/main/10.2/index.html#//00s90000003m000000)?

_Tools_ for creating _mapbooks_ using _feature classes_ 

(basically)

# _What_ is [arcpy](http://resources.arcgis.com/en/help/main/10.2/index.html#//000v000000v7000000)?

Esri [python](https://www.python.org/) library for _geoprocessing_ and _other_ tasks

# Project Goals

Retain _80-90%_ of original maps' features

Remain _flexible_

Greatly _reduce_ production time

# Example _New_ System Map

![](./Images/AST4_New.png)

# How does it work?

Data Driven Pages drive the _map_ using our _custom grids_

![](./Images/DialogDDP.png)

_Grid_ feature class' attributes _drive_ the dynamic content

A _point_ feature class stores info for _detail insets_

![](./Images/DrivingTables.png)

MXD layout:

![](./Images/Layout_Screenshot.png)

# Process' Steps 

For Each _Mapbook_ Selected:

Empty _PDF_ generated

_Symbology_ set up via _definition queries_

For Each _Page_:

Map _text elements_ updated

_Inset elements_ moved onto layout (as needed)

(_Zoom_ to specified _feature & scale_)

Temp _PDF_ for _page_ created

Temp _page_ added to _empty PDF_

# Pros:

_ONE_ mxd to manage!

Can produce _several_ pages a day

_Standardized_ map layout

# Cons:

_Limited_ number of _insets_ per page

Can be _difficult_ to make _well laid-out_ insets

_Non-network_ features _can't_ easily be symbolized by _network_ ID

(selection set layers formerly)

_Extra_ paper usage

# Another _Cool_ Feature Implemented

_Dynamically generated_ picklist!

![](./Images/ScriptToolDialog.png)

_Unique value list_ derived from a feature class

Achieved through modifying the script's _validation_ code

![](./Images/ScriptValidation.png)

```python
def updateParameters(self):
  FC = r"<path to breakers feature class>"
  Col = "FeederID"
  self.params[0].filter.list = [
    str(val) for val in sorted(
      set(
        row.getValue(Col) for row in arcpy.SearchCursor(FC, None, None, Col)
      )
    )
  ]    
  return
```

# Questions?

_Thank you!_

* [msayler@clarkpud.com](mailto:msayler@clarkpud.com)
* &nbsp;
* [github.com/mattsayler](https://www.github.com/mattsayler)
