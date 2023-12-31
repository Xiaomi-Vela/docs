# 多HAP使用规则


- App Pack包不能直接安装到设备上，只是上架应用市场的单元。

- App Pack包打包时会对每个HAP在json文件中的配置进行校验，确保bundleName、versionCode等标签取值相同，详见[App打包时的HAP合法性校验](../tools/packing-tool.md#app打包指令)。

- App Pack包中同一设备类型的所有HAP中必须有且只有一个Entry类型的HAP，Feature类型的HAP可以有一个或者多个，也可以没有。

- App Pack包中的每个HAP必须配置moduleName标签，同一设备类型的所有HAP对应的moduleName标签必须唯一。

- 同一应用的所有HAP签名证书要保持一致。上架应用市场是以App Pack的形式上架，并对其进行了签名。应用市场分发时会将所有HAP从App Pack中拆分出来，同时对其中的所有HAP进行重签名，这样保证了所有HAP签名证书的一致性。在调试阶段，开发者通过命令行或IDE将HAP安装到设备上时要保证所有HAP签名证书一致，否则会出现安装失败的问题。
