# Native API Document Comments

> **NOTE**
>
> Native API reference documents are generated by header files that comply with the comment specifications stipulated in this topic.

## Module Comments

```
/**
 * @addtogroup Module name
 * @{
 * 
 * @brief Outline the functionality of the module in one sentence.
 * 
 * Describe the main functionalities, use scenarios, and use suggestions of the module. Focus on the logical concepts involved in this module, their relationships, and their functionalities in an application.
 * For example, for choreographer, describe its functionalities and how to use it.
 * Choreographer orchestrates the timing of frame rendering. It is a C implementation in Java. Applications can use choreographer to arrange the proper timing of frame rendering as follows:
 * 1. Register a callback function with choreographer.
 * 2. The callback function is called when it is time to start the next frame, with the FrameCallbackData parameter returned.
 * 3. Perform processing on the callback.
 * 4. The SF performs conversion based on the return value of the callback.
 * In the detailed description, if there are multiple paragraphs, end each paragraph with \n.\n
 *
 * @since OS version
 */

...

/** @} */ (If specific functions in the header file need to be classified into this module, add /** @} */ to the end of the file.) */
```

## File Comments

```
/**
 * @file Header file name
 * 
 * @brief Outline the functionality of the header file in one sentence.
 *
 * Describe the main functionalities, use scenarios, and use suggestions of this class or interface. Focus on the logical concepts involved in this class, their relationships, and their functionalities in an application.\n
 * In the detailed description, if there are multiple paragraphs, end each paragraph with \n.\n
 * @library Name of the .so file to be linked when the header file interface is referenced
 * @since OS version
 */
```

## Macro Definition/Variable/Constant Comments

```
/**
 * @brief Outline the meaning of the macro definition, constant, or variable in one sentence.
 *
 * Describe the functionalities, use restrictions, use suggestions, and value ranges of the macro definition, constant, and variable, as well as consequences when boundary values and invalid values are used.\n
 * In the detailed description, if there are multiple paragraphs, end each paragraph with \n.\n
 * 
 * @deprecated (Optional) Add this flag for a deprecated interface. Specify the version from which the interface is deprecated and the substitute interface.
 * @since OS version
 */
```

## Struct and Union Comments

```
/**
 * @brief Outline the functionality of the struct or union in one sentence.
 * 
 * Describe the functionalities, use scenarios, and use suggestions of the struct or union.\n
 * In the detailed description, if there are multiple paragraphs, end each paragraph with \n.\n
 * 
 * @deprecated (Optional) Add this flag for a deprecated interface. Specify the version from which the interface is deprecated and the substitute interface.
 * @since OS version
 */
struct StructName { 
/** Describe the meaning of member 1. */
unsigned long StructMember1;
/** Describe the meaning of member 2. */
unsigned long StructMember2;
};
```

## Enum Comments

```
/**
 * @brief Outline the functionality of the enum in one sentence.
 *
 * Describe the main functionalities, use scenarios, and use suggestions of the enum.\n
 * In the detailed description, if there are multiple paragraphs, end each paragraph with \n.\n
 * 
 * @deprecated (Optional) Add this flag for a deprecated interface. Specify the version from which the interface is deprecated and the substitute interface.
 * @since OS version
 */
enum EnumName {
    /** Describe the meaning of the enumerated value 1. */
    EnumMermber1,  
    /** Describe the meaning of the enumerated value 2. */
    EnumMermber2, 
    /** Describe the meaning of the enumerated value 3. */
    EnumMermber3 
}; 
```

## Function Comments

```
/**
 * @brief Outline the functionality of the function in one sentence.
 *
 * Describe the main functionalities, use scenarios, and use suggestions of the function.\n
 * In the detailed description, if there are multiple paragraphs, end each paragraph with \n.\n
 * 
 * @param (Optional) Followed by the parameter name and description. Use one @param tag for each parameter. If the function does not have parameters, delete the tag. Content of the parameter description: 1. Parameter functionality, use restrictions, and use suggestions; 2. Value range of the parameter, and consequences when boundary values and invalid values are used; 3. Recommended or empirical values
 * @return (Optional) Followed by the return value description. If the function does not return a value, delete the tag.
 * @see (Optional) Followed by a function associated with the current function. Use one @see tag for each associated function. If the current function does not have associated functions, delete the tag.
 * @permission (Optional) Followed by the permission required to use the function. Use one @permission tag for each associated permission. If the function does not require any permission, delete the tag.
 * @deprecated (Optional) Add this flag for a deprecated interface. Specify the version from which the interface is deprecated and the substitute interface.
 * @since OS version
 */
```