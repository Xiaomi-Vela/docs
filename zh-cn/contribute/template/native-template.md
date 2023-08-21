# Native接口文档注释

> **说明：** 
>
> Native API文档由中文头文件生成，中文头文件应遵循以下注释规范才能生成对应文档。

## Module的注释

```
/**
 * @addtogroup 模块名
 * @{
 * 
 * @brief 一句话描述该库的作用。（请使用动宾结构，如：实现XX功能。）
 * 
 * 详细描述该模块的主要功能、使用场景和使用建议。尤其对这个模块中涉及的逻辑概念，相互关系，在应用中的作用进行说明。
 * 介绍这个概念的功能；然后介绍下简单的使用方法
 * 详细描述中，如果有多个段落，每段必须以“\n”结束。\n
 *
 * @since OS的版本号
 */

...

/** @} */ (如果需要将头文件中具体函数划分到该模块中，则在文件最后加上/** @} */ )
```

## 文件File的注释

```
/**
 * @file 头文件名
 * 
 * @brief 一句话简要描述该头文件的作用。
 *
 * 详细描述该类或接口的主要功能、使用场景和使用建议。覆盖该类的主要功能、使用场景和使用建议。尤其对这个类涉及的逻辑概念，相互关系，在应用中的作用进行说明。\n
 * 详细描述中，如果有多个段落，每段必须以“\n”结束。\n
 * @library 引用头文件接口，需要链接的so名字
 * @syscap 后面跟着这个头文件属于的syscap能力
 * @since OS的版本号
 */
```

## 宏定义/变量/常量的注释

```
/**
 * @brief 一句话简要描述该宏定义/常量/变量的含义。
 *
 * 详细描述该宏定义/常量/变量的作用、使用限制和建议、取值范围，以及取到边界值、非法值的后果。\n
 * 详细描述中，如果有多个段落，每段必须以“\n”结束。\n
 * 
 * @deprecated （可选）since OS的版本号 标记从什么版本开始废弃此变量，后面需要写明使用替代的方法
 * @since OS的版本号
 */
```

## 结构体Struct和联合体Union的注释

```
/**
 * @brief 一句话简述该结构体或联合体的作用。
 * 
 * 详细描述该结构体或联合体的作用、使用场合和建议等。\n
 * 详细描述中，如果有多个段落，每段必须以“\n”结束。\n
 * 
 * @deprecated （可选）since OS的版本号；标记位废弃的接口，需要加上这个标记，后面写明从什么版本开发废弃,使用什么接口代替
 * @since OS的版本号
 */
struct StructName { 
/** 描述成员1的含义。 */
unsigned long StructMember1;
/** 描述成员2的含义。 */
unsigned long StructMember2;
/** 描述成员3的含义。 
 * @since（可选） OS版本号，当新增域时，与结构体总的引入版本号不一样的时候，需要写上since，表明这个域新增版本。
 */
unsigned long StructMember3;
};
```

## 枚举Enum的注释

```
/**
 * @brief 一句话简述该枚举的作用。
 *
 * 详细描述该枚举的主要功能、使用场景和使用建议。\n
 * 详细描述中，如果有多个段落，每段必须以“\n”结束。\n
 * 
 * @deprecated （可选）since OS的版本号；标记位废弃的接口，需要加上这个标记，后面写明从什么版本开发废弃,使用什么接口代替
 * @since OS的版本号
 */
enum EnumName {
    /** 描述枚举值1的含义 */
    EnumMermber1,  
    /** 描述枚举值2的含义 
     * @deprecated（可选） since OS的版本号；当需要废弃某个枚举值，需要标记从什么版本开始废弃。废弃后不要删除，尤其是顺序编码的枚举值，删除后会导致枚举值变化。
     */
    EnumMermber2, 
    /** 描述枚举值3的含义
     * @since（可选） OS版本号，当新增枚举值时，与结构体总的引入版本号不一样的时候，需要写上since，表明这个域新增版本 
     */
    EnumMermber3 
}; 
```

## 函数Function的注释

```
/**
 * @brief 一句话简述该函数的作用。
 *
 * 详细描述该函数的主要功能、使用场景和使用建议。\n
 * 详细描述中，如果有多个段落，每段必须以“\n”结束。\n
 * 
 * @param （可选）后接参数名和参数描述，一个参数使用一个@param标记。参数描述写作要点：1.参数的作用、使用限制和建议；2.参数的取值范围，以及取到边界值、非法值的后果；3.如果存在参数设置方面的建议值或经验值，请描述。如果该方法没有参数，则请删除该标记。
 * @return （可选）后接返回描述，对此函数会返回的每个返回值进行详细说明其含义。如果该函数没有返回值，则请删除该标记。
 * @see （可选）当存在与该函数相关联的函数时（功能相近或者存在关系），可以通过@see建立到参考函数的链接。如果需要链接多个函数，每个函数使用一个@see标记。如果不涉及，则请删除该标记。 
 * @permission （可选）对权限有要求的接口需要写
 * @deprecated （可选）since OS的版本号；标记位废弃的接口，需要加上这个标记，并写明从什么版本开发废弃
 * @useinstead  使用什么接口代替
 * @since OS的版本号
 */
```