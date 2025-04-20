<h1 align="center">
  Universal Converter 
</h1>

<p align="center">
   一款通用的订阅转换工具
</p>

## 📌 支持代理工具

| 🔨代理工具                | 💻️运行平台 | [📄 转换配置文件](#-转换配置文件) |
| ---------------------- | :------: | :--------------: |
| Clash Verge For Windows|   Windows     |Clash.ini|
| Clash Verge For MAC    |     Mac       |Clash.ini|
| Clash Meta For Android |   Android     |Clash.ini|
| Stash                  |     IOS       |Stash.ini|
| OpenClash              |   OpenWrt     |Clash.ini|
| SingBox                |     Any       |SingBox.ini|

## 🚥 支持输入订阅类型

| 类型                  | 作为源类型 |
| ---------------------- | :---: | 
| V2Ray                  |   ✓   |
| Clash                  |   ✓   |


## 🤸 调用说明

| 调用参数   | 必要性 | 示例                        | 解释                                                                                                                  |
| ------ | :-: | :------------------------ | ------------------------------------------------------------------------------------------------------------------- |
| [NAME](#调用参数name)   |  可选 | NAME=ActionRobotAI      |  生成的配置文件名称，不填则默认名称为 Subscribe                                                                                        |
| [CFG](#调用参数cfg)    |  可选 | CFG=Clash.ini            | 转换配置文件的来源地址 (包含节点分组和代理规则)，远程转换配置需要经过 [URL编码](https://www.urlencoder.org/) 处理，当此参数不存在时默认使用 Clash.ini|
| [URL](#调用参数url)    |  必要 | URL=https%3A%2F%2Fwww.xxx.com | 代理节点的来源地址，需要经过 [URL编码](https://www.urlencoder.org/) 处理                              |
| [公共可选参数](#调用参数公共可选参数)|  可选 | 公共可选参数=参数值 | 转换配置中的公共可选参数，从请求链接传递的参数优先级要高于CFG参数指定的转换配置文件中的参数                              |



-   ### 示例用法:

    ```
    http://127.0.0.1:5000/universalconverter?CFG=Clash.ini&URL=%SubcribeURL%
    ```
    **💡 各个调用参数之间使用 `&` 符号进行连接**
-   ### 调用参数(NAME)

    此参数可以设置此次转换生成的代理配置文件名称，在代理软件存在多个订阅时可区分不同订阅或机场标识
    **⚠️请勿在名称中添加文件名后缀，程序依照转换配置文件中的目标平台类型，自动添加文件后缀名(Clash.ini会添加.yaml后缀、SingBox.ini会添加.json后缀)**

    -   #### 示例用法:

        ```
        NAME=ActionRobotAI
        ```
        **默认值:Subscribe**
-   ### 调用参数(CFG)
    **此参数可以设置此次转换所参照的转换配置文件，为不同代理工具生成不同格式的代理文件**
    具体转换配置文件的格式以及写法参见 [📄 转换配置文件](#-转换配置文件)

    -   **调用服务器本地转换配置文件**
    
         服务器本地订阅文件 `Clash.ini`
        -   **示例用法**

            ```
            CFG=Clash.ini
            ```
            **⚠️ 要调用服务器本地转换配置文件，请将转换配置文件存放在程序运行目录`./Config`文件夹下**
    -   **调用远程转换配置文件**
      
        远程转换配置文件链接 `https://www.xxx.com`
        -   **示例用法**

            链接经过[URL编码](https://www.urlencoder.org/)后
            
            ```
            CFG=https%3A%2F%2Fwww.xxx.com
            ```
    -   **默认值:Clash.ini**
-   ### 调用参数(URL)

    **此参数可以设置此次转换的代理节点来源**

    -   #### 单条代理节点来源

        -   **远程订阅连接**
            远程订阅链接 `https://www.xxx.com`
            -   **示例用法**

                链接经过[URL编码](https://www.urlencoder.org/)后
                ```
                URL=https%3A%2F%2Fwww.xxx.com
                ```
        -   **指定订阅连接的User-Agent**

            远程订阅链接 `https://www.xxx.com` 要求以`clash`作为User-Agent来请求订阅文件
            -   **书写格式**
                ```
                URL=SubscribeURL^User-Agent
                ```
            -   **示例用法**

                链接经过[URL编码](https://www.urlencoder.org/)后
                ```
                URL=https%3A%2F%2Fwww.xxx.com%5eclash
                ```  
            -   **默认值:v2ray**
            **⚠️ User-Agent应当使用[🚥 支持的输入订阅类型](#-支持输入订阅类型) ，如`clash`、`v2ray`、`clash-verge`**
        -   **V2Ray格式的节点信息**

            节点信息 `vless://ae696e8f-a124-4c2b-8fb9-732b64cdc13c@1.1.1.1:1234?type=tcp#Vless`
            -   **示例用法**

                经过[URL编码](https://www.urlencoder.org/)后
                ```
                URL=vless%3A%2F%2Fae696e8f-a124-4c2b-8fb9-732b64cdc13c%401.1.1.1%3A1234%3Ftype%3Dtcp%23Vless
                ```
        -   **服务器本地订阅文件**

            服务器本地订阅文件 `Subscribe.yaml`
                
            -   **示例用法**
                ```
                URL=Subscribe.yaml
                ```
                **⚠️ 要调用服务器本地的订阅文件，请将订阅文件存放在程序运行目录`./Subscribe`文件夹下** 
    -   #### 多条代理节点来源
        合并以下代理节点来源：
        -   1.远程订阅链接 `https://www.A.com`
        -   2.远程订阅链接 `https://www.B.com`，请求User-Agent为`V2Ray`
        -   3.服务器本地订阅文件 `Subscribe.yaml`
        -   4.V2Ray格式的节点信息 `vless://ae696e8f-a124-4c2b-8fb9-732b64cdc13c@1.1.1.1:1234?type=tcp#Vless`
        -   **示例用法**

            **💡 远程订阅链接和V2Ray格式的单节点信息分别经过[URL编码](https://www.urlencoder.org/)后，使用 `|` 符号拼接合并**
            ```
            URL=https%3A%2F%2Fwww.A.com|https%3A%2F%2Fwww.B.com%5eV2Ray|Subscribe.yaml|vless%3A%2F%2Fae696e8f-a124-4c2b-8fb9-732b64cdc13c%401.1.1.1%3A1234%3Ftype%3Dtcp%23Vless
            ```
        **⚠️ 当多份订阅节点中的节点名称冲突时，程序将自动为名称重复的节点名称后增加`_`以防止节点重复**

-   ### 调用参数(公共可选参数)

    **⚠️ 这些参数未来可能会增加或删除或修改，且会与转换配置文件中的公共参数融合共同完成转换任务**

    -   **ProxyNodeUDP (bool)**
        -   `true`:强制启用所有代理节点的 UDP 参数
        -   `fasle`:强制关闭所有代理节点的 UDP 参数
        -   `不写或空值`:不对代理节点进行任何处理
        ```
        ProxyNodeUDP=true
        ```
    -   **ProxyNodeSCV (bool)**
        -   `true`:强制启用所有代理节点的 SkipCertVerify 参数
        -   `fasle`:强制关闭所有代理节点的 SkipCertVerify 参数
        -   `不写或空值`:不对代理节点进行任何处理
        ```
        ProxyNodeSCV=true
        ```
    -   **ProxyNodeTFO (bool)**
        -   `true`:强制启用所有代理节点的 TCP Fast Open 参数
        -   `fasle`:强制关闭所有代理节点的 TCP Fast Open 参数
        -   `不写或空值`:不对代理节点进行任何处理
        ```
        ProxyNodeTFO=true
        ```
    -   **ProxyNodeVMESSAEAD (bool)**
        -   `true`:强制所有Vmess代理节点的 alterId 参数为0
        -   `fasle`:不对代理节点进行任何处理
        -   `不写或空值`:不对代理节点进行任何处理
        ```
        ProxyNodeVMESSAEAD=true
        ```
    -   **ProxyRuleNoResolve (bool)**
        -   `true`:强制为所有IP类和规则集类的代理规则添加 no-resolve 属性，这会展开引用的本地.list文件进行处理。
        -   `fasle`:不对代理规则进行任何处理
        -   `不写或空值`:不对代理规则进行任何处理
        ```
        ProxyRuleNoResolve=true
        ```

## 📄 转换配置文件
**转换配置文件`XXX.ini`，用于配置转换的详细过程和参数**
-   ### GeneratedConfig
    转换配置文件的参数
    - #### 转换配置文件专用参数
        -   **TargetPlatform(string 必须)**

            目标代理工具类型 如 `Clash`、`Singbox`

            ```
            TargetPlatform=Clash
            ```    
            **⚠️ 务必正确填写代理工具的类型，否则可能会生成错误的代理文件**
        -   **ProxyNodeNameExclude(string 可选)**

            依照节点名称过滤机场节点中的无用节点，如套餐流量信息、机场官网地址、机场TG群组等，过滤器用法参见  [⚗ 节点过滤器](#-节点过滤器)
            

            ```
            ProxyNodeNameExclude=(官网|流量|套餐|剩余|到期|电报群|http|tg)
            ```    
                  
    - #### 转换配置文件的公共可选参数
        参见 [调用参数(公共可选参数)](#调用参数公共可选参数)

        **⚠️ 转换配置文件中的公共可选参数优先级低于从请求链接中传递的公共可选参数，请求链接中的公共可选参数将会覆盖转换配置文件中的公共可选参数**

-   ### GeneratedTemplate
    转换配置文件的生成模板，此模板内容应当与`TargetPlatform`参数所指定的目标类型相对应。
-   ### ProxyGroup
    转换配置文件的节点分组
    -   **书写格式**
        ```
        ProxyGroup=节点组名称`节点组类型`节点过滤器或节点组1,节点过滤器或节点组2,...,节点过滤器或节点组N`延迟测试URL`延迟测试间隔s`切换容差ms
        ```
    -   **节点组名称**

        要求：不包含特殊字符，但可使用Emoji和空格
    -   **节点过滤器或节点组**

        节点过滤器或节点组之间要用 `,` 符号分割开
        -   **节点组**
            ```
            []🔰 节点选择
            ```
        -   **关键字节点组**
            ```
            []DIRECT
            []REJECT
            ```    
            **⚠️ REJECT 在SingBox中不能作为节点或节点组进行分组**
        -   **节点过滤器**

            参见 [⚗ 节点过滤器](#-节点过滤器)
        -   **所有节点**
            ```
            .*
            ```
    -   **节点组类型**
        -    **select**

                ```
                🇭🇰 香港节点`select`(🇭🇰|HK|Hongkong|香港|港)
                ```   
        -    **url-test**  

                ```
                🇭🇰 香港节点(自动)`url-test`(🇭🇰|HK|Hongkong|香港|港)`http://www.gstatic.com/generate_204`600`150
                ```  
    -   **延迟测试URL**  

        文本  进行节点延迟测试的URL         
    -   **延迟测试间隔**

        数字 单位为s秒
    -   **延迟测试间隔**

        数字 单位为ms毫秒
-   ### ProxyRule
    转换配置文件的代理规则，代理规则遵循自上而下的顺序生成。
    -   **原生规则内容(⚠️ SingBox 无效)**
    

        直接书写原生规则，规则会被直接复制到代理配置文件中不会进行任何处理。



        -   **书写格式**
            ```
            ProxyRule=原生规则内容
            ``` 
        -   **示例用法**
        
            ```
            ProxyRule=AND,((DST-PORT,443),(NETWORK,UDP)),REJECT
            ``` 
    -   **本地规则文件.list**
        -   **书写格式**
            ```
            ProxyRule=节点组名称`本地规则文件相对路径
            ```
        -   **示例用法**
        
            ```
            ProxyRule=🎥 Netflix`Rule/Clash/Netflix/Netflix.list
            ```  
    -   **远程规则集**

         -   **书写格式**

                ```
                ProxyRule=节点组名称`[]远程规则集URL,远程规则集文件格式:远程规则集行为类型,下载远程规则集所使用的节点组,规则集刷新时间s`是否不进行域名解析

                ProxyRule=outbound`[]ruleseturl,format:behavior
                ProxyRule=outbound`[]ruleseturl,format:behavior,proxy
                ProxyRule=outbound`[]ruleseturl,format:behavior,proxy,interval
                ProxyRule=outbound`[]ruleseturl,format:behavior,proxy,interval`no-resolve

                ProxyRule=outbound`[]ruleseturl,format
                ProxyRule=outbound`[]ruleseturl,format,proxy
                ProxyRule=outbound`[]ruleseturl,format,proxy,interval
                ProxyRule=outbound`[]ruleseturl,format,proxy,interval`no-resolve
                ```
        -   **示例用法**
        
            ```
            ProxyRule=🎯 全球直连`[]https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/refs/heads/master/rule/Clash/ChinaMaxNoIP/ChinaMaxNoIP_Domain.yaml,yaml:domain,♻️ 自动选择,86400`no-resolve
            ProxyRule=🛑 广告拦截`[]https://raw.githubusercontent.com/SagenNet/sing-geosite/rule-set/geosite-geolocation-!cn.srs,binary,♻️ 自动选择,86400
            ProxyRule=REJECT`[]https://raw.githubusercontent.com/SagenNet/sing-geosite/rule-set/geosite-geolocation-!cn.srs,binary,♻️ 自动选择,86400
            ```     
    -   **GEOX集规则**
        -   **书写格式**
            ```
            ProxyRule=节点组名称`[]GEOX,规则集子集`是否不进行域名解析
            ```
        -   **示例用法**
        
            ```
            ProxyRule=🔰 节点选择`[]GEOSITE,!CN
            ProxyRule=🔰 节点选择`[]GEOIP,!CN`no-resolve
            ```  
    -   **终结点规则**
        -   **书写格式**
            ```
            ProxyRule=节点组名称`[]终结点
            ```
        -   **示例用法**
        
            ```
            ProxyRule=🐟 漏网之鱼`[]FINAL
            ```  

## ⚗ 节点过滤器

-   ### 输入

    -   **所有节点名称列表**

    -   **过滤器表达式**

-   ### 输出

    -   **过滤后的节点列表。**

        💡 节点过滤器作用于节点分组过滤时，输出将会是节点的名称而不会输出节点组的名称。

-   ### 过滤器表达式
    节点过滤器的表达式使用 `&`与 `|`或 `!`非 以及`(` `)`闭合括号 的逻辑规则，其语法类似`if判断表达式`那样便于书写与理解，且支持与`正则表达式`联合使用。
    -   **常规表达式**

        -   **筛选香港节点**

            ```
            (🇭🇰|HK|Hongkong|香港|港)
            ```

        -   **筛选日本节点**

            仅使用并集筛选会导致 `尼日利亚` 进入日本节点组，需要排除包括 `利亚` 字段的节点 

            ```
            (!利亚)&(🇯🇵|JP|Japan|日本|日|东京|大阪|泉日|埼玉|沪日|深日)
            ```

        -   **在香港节点中筛选奈飞节点**

            ```
            (🇭🇰|HK|Hongkong|香港|港)&(奈飞|Netflix)
            ```
    -   **流量倍率表达式**      
        -   **书写格式**
            `大小比较符` `倍率数字` 两者左右顺序不可变
            ```
            (<=2.0)
            (>=1.0)
            ```  
        -   **在香港节点中筛选流量倍率低于2.0的节点**

            ```
            (<=2.0)&(🇭🇰|HK|Hongkong|香港|港)
            ```
    -   **正则表达式**          
        -   **书写格式**
            ```
            REGEX:BASE64编码后的正则表达式
            ```
        -   **使用正则表达式筛选日本节点**

            筛选日本节点的标准正则表达式

            ```
            ^(?!.*利亚).*(🇯🇵|JP|Japan|日本|日)
            ```
            正则表达式经过[BASE64编码](https://www.base64encode.org/)后
            ```
            Xig/IS4q5Yip5LqaKS4qKPCfh6/wn4e1fEpQfEphcGFufOaXpeacrHzml6Up
            ```
            最后按照书写格式组合
            ```
            REGEX:Xig/IS4q5Yip5LqaKS4qKPCfh6/wn4e1fEpQfEphcGFufOaXpeacrHzml6Up
            ```
        -   **使用正则表达式与其他规则联合筛选流量倍率大于2.0日本节点**


            筛选日本节点的标准正则表达式

            ```
            ^(?!.*利亚).*(🇯🇵|JP|Japan|日本|日)
            ```
            正则表达式经过[BASE64编码](https://www.base64encode.org/)后
            ```
            Xig/IS4q5Yip5LqaKS4qKPCfh6/wn4e1fEpQfEphcGFufOaXpeacrHzml6Up
            ```
            最后按照书写格式组合
            ```
            (>=2.0)&(REGEX:Xig/IS4q5Yip5LqaKS4qKPCfh6/wn4e1fEpQfEphcGFufOaXpeacrHzml6Up)
            ```            
<!-- 更新时间: Sun Apr 20 02:00:16 UTC 2025 -->
