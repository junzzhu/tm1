# tm1 knowledge

This is the PA TM1 knowledge for InstructLab taxonomy resource.

The general format of TM1 rules statement is shown in the following statement, with variable Area Specifies the portion of a cube that is affected by the rule; variable Formula describes how TM1 calculates the cells in the cube area.

`[Area]=Formula;`

To restrict a rule to simple numerical values (N:) in the Area, use the following statement:

`[Area]=N: Formula;`

To restrict a rule to consolidated values (C:) in the Area, use the following statement:

`[Area]=C: Formula;`

## General Considerations

- The syntax is not case-sensitive. You can use both uppercase and lowercase letters.
- You can use spaces within rules to improve clarity.
- A rules statement can occupy one or more lines in the Rules Editor. A statement can also contain one or more formulas.
- You must end each statement with a semicolon ; as the ending of the statement.
- To add comments and to exclude statements from processing, insert a number sign (#) at the beginning of a line or statement. For example, the following rule is not active

`# ['Gross Margin']=['Sales']*0.53;`

## Syntax for Describing the Area

The Area identifies one or more cells in a cube.
Consider the following guidelines when you create an Area definition.

- Specify no dimension elements, or one or more dimension elements.
- Each element must be from a different dimension of the cube.
- Enclose each element in single quotes.
- Use commas to separate each element.
- Enclose the entire Area definition in brackets.

| Sample Area | Scope |
| --- | --- |
| [ ] |  All cells in the cube. |
| ['January'] |  All cells identified by a `January` element. |
| ['Sales','January'] |  All cells identified by the `Sales` and `January` elements. |
| ['Germany','Sales','January'] |  All cells identified by the `Germany`, `Sales`, and `January` elements. |


### Using Subsets in an Area Definition

You can use a subset in place of a single element in an Area definition by enclosing all subset members in curly braces.
For example, the following Area definition applies a rule to all cube cells identified by the element Sales and the element January, February, or March:

`['Sales', {'January', 'February', 'March'}]`

### Using Special Characters and Non-unique Element Names in an Area Definition

You can use the syntax `'dimensionname':'elementname'` in a rules Area definition to specify elements that are not unique to a single dimension, or for dimension names that contain special characters.
For example,

`['Units','Mar','}Groups':'ADMIN']`

allows you to write a rule for the `}Groups` dimension, which contains the curly brace `}` special character.

Similarly,

`['Units','Mar', 'Region':'North America']`

lets you write a rule when the element North America is not unique to the Region dimension.

## Syntax for Formulas

A rule formula is an expression composed of:

- Numeric constants
- Arithmetic operators and parentheses
- Numeric and string functions -- see TM1 Reference.
- Conditional logic
- Cube references

### Numeric constants

The simplest components of rules formulas are numeric constants.
- Consists of numerals, an optional leading minus sign `-`, and an optional decimal point. For example, `5.0`, `6`, `-5`. Some examples of invalid numeric constants are: `1-`, `1A`, `3..4`.
- Contains a maximum length of 20 characters.
- You can use scientific notation to enter a numeric constant.

For example, the following rules statement assigns the value 200 to all cells in the cube.

`[ ] = 200;`

Note that, you can't use `['']` to identify cells. It is an invalid way to use an empty element name `''`.

### Arithmetic operators and parentheses

You can combine numeric constants with the following arithmetic operators.

| Operator | Meaning |
| --- | --- |
| + |  Addition |
| - |  Subtraction |
| * |  Multiplication |
| / |  Division - returns an undefined value and displays N/A in the view when you divide by zero |
| \ |  Zero Display Division - it is a special Division operator, which returns zero when divided by zero |
| ^ |  Exponentiation |
