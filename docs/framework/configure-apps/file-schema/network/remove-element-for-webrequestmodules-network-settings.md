---
title: '&lt;削除&gt;webRequestModules (ネットワーク設定) の要素'
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/webRequestModules/remove
- http://schemas.microsoft.com/.NetConfiguration/v2.0#remove
helpviewer_keywords:
- remove element, webRequestModules
- webRequestModules, remove element
- <remove> element, webRequestModules
- <webRequestModules>, remove element
ms.assetid: dd84d2fe-2f4f-457a-9d3c-441d0d21cc10
author: mcleblanc
ms.author: markl
manager: markl
ms.openlocfilehash: 40eda14d4d578f10a77aa06843abd48f58c55f6a
ms.sourcegitcommit: 9e18e4a18284ae9e54c515e30d019c0bbff9cd37
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2018
ms.locfileid: "37073022"
---
# <a name="ltremovegt-element-for-webrequestmodules-network-settings"></a>&lt;削除&gt;webRequestModules (ネットワーク設定) の要素
アプリケーションからカスタム Web 要求のモジュールを削除します。  
  
 \<configuration>  
\<system.net>  
\<webRequestModules>  
\<remove>  
  
## <a name="syntax"></a>構文  
  
```xml  
<remove   
  prefix="URI prefix"   
/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|**属性**|**説明**|  
|-------------------|---------------------|  
|`prefix`|この Web 要求モジュールによって処理される要求の URI プレフィックス。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|[webRequestModules](../../../../../docs/framework/configure-apps/file-schema/network/webrequestmodules-element-network-settings.md)|使用してネットワークのホストから情報を要求するモジュールを指定します。|  
  
## <a name="remarks"></a>Remarks  
 `remove`要素が指定した URI プレフィックスの登録済みの Web 要求のモジュールを削除します。  
  
 値、`prefix`属性が有効な URI: たとえば、"http"の先頭の文字にする必要がありますか"`http://www.contoso.com` "です。  
  
## <a name="configuration-files"></a>構成ファイル  
 この要素は、アプリケーション構成ファイルまたはマシン構成ファイル (Machine.config) で使用できます。  
  
## <a name="example"></a>例  
 次の例では、HTTP の場合、既存の Web 要求のモジュールを削除し、www.contoso.com への HTTP 要求のカスタム Web 要求の新しいモジュールを登録します。  
  
```xml  
<configuration>  
  <system.net>  
    <webRequestModules>  
      <remove prefix="http">  
      <add prefix="http"  
           type="System.Net.HttpRequestCreator, System, Version=2.0.3600.0,  
           Culture=neutral, PublicKeyToken=b77a5c561934e089"  
      />  
    </webRequestModules>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Net.WebRequest>  
 [ネットワーク設定スキーマ](../../../../../docs/framework/configure-apps/file-schema/network/index.md)
