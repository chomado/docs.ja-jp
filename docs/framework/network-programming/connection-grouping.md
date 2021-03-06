---
title: 接続のグループ化
ms.date: 03/30/2017
helpviewer_keywords:
- Internet, connections
- connections [.NET Framework], grouping
- WebRequest class, connection grouping
- network resources, connections
- connection pooling
ms.assetid: 2ec502e8-4ba0-4c22-9410-f28eaf4eee63
author: mcleblanc
ms.author: markl
manager: markl
ms.openlocfilehash: bbf34f1e653e95ea30a3e9945fc74c99cfdc3a45
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33395048"
---
# <a name="connection-grouping"></a>接続のグループ化
接続のグループ化では、1 つのアプリケーション内の特定の要求を定義済みの接続プールに関連付けます。 これは、ユーザーの代わりにバック エンド サーバーに接続し、デリゲートをサポートする認証プロトコル (Kerberos など) を使用する中間層アプリケーションや、以下の例のように、独自の資格情報を指定する中間層アプリケーションで必要になる場合があります。 たとえば、Joe というユーザーが、自分の給与情報を表示する内部 Web サイトにアクセスするとします。 Joe の認証後、中間層アプリケーション サーバーは、Joe の資格情報を使用してバック エンド サーバーに接続し、Joe の給与情報を取得します。 次に、Susan がサイトにアクセスし、自分の給与情報を要求します。 中間層アプリケーションが Joe の資格情報を使用して既に接続しているため、バック エンド サーバーは Joe の情報で応答します。 ただし、アプリケーションがバック エンド サーバーに送信される各要求をユーザー名から形成される接続グループに割り当てると、各ユーザーは個別の接続プールに属すことになり、誤って他のユーザーと認証情報を共有することがなくなります。  
  
 要求を特定の接続グループに割り当てるには、要求を行う前に、<xref:System.Net.WebRequest> の <xref:System.Net.WebRequest.ConnectionGroupName%2A> プロパティに名前を割り当てる必要があります。  
  
## <a name="see-also"></a>参照  
 [接続の管理](../../../docs/framework/network-programming/managing-connections.md)  
 [方法: グループの接続にユーザー情報を割り当てる](../../../docs/framework/network-programming/how-to-assign-user-information-to-group-connections.md)
