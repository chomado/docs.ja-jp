---
title: XslCompiledTransform クラスの使用
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: f9b074f6-d6f4-49dd-a093-df510bf0cf7b
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6b242556e6fb05cae5ff5f54d1b134e1db918e5b
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33571047"
---
# <a name="using-the-xslcompiledtransform-class"></a>XslCompiledTransform クラスの使用
<xref:System.Xml.Xsl.XslCompiledTransform> クラスは Microsoft .NET Framework XSLT プロセッサです。 このクラスは、スタイル シートをコンパイルし、XSLT 変換を実行するために使用されます。  
  
> [!NOTE]
>  全体的なパフォーマンスは <xref:System.Xml.Xsl.XslCompiledTransform> クラスの方が <xref:System.Xml.Xsl.XslTransform> クラスより優れていますが、<xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> クラスの <xref:System.Xml.Xsl.XslCompiledTransform> メソッドが変換で初めて呼び出されたときは、<xref:System.Xml.Xsl.XslTransform.Load%2A> クラスの <xref:System.Xml.Xsl.XslTransform> メソッドよりパフォーマンスが劣る場合があります。 これは、XSLT ファイルを読み込む前にコンパイルする必要があるためです。 詳しくは、ブログの投稿「[XslCompiledTransform Slower than XslTransform?](https://blogs.msdn.microsoft.com/antosha/2006/07/16/xslcompiledtransform-slower-than-xsltransform/)」(XslCompiledTransform は XslTransform より遅い?) をご覧ください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [XslCompiledTransform クラスへの入力](../../../../docs/standard/data/xml/inputs-to-the-xslcompiledtransform-class.md)  
 使用可能な XSLT 入力オプションについて説明します。  
  
 [XslCompiledTransform クラスの出力オプション](../../../../docs/standard/data/xml/output-options-on-the-xslcompiledtransform-class.md)  
 使用可能な XSLT 出力オプションについて説明します。  
  
 [XSLT 処理中の外部リソースの解決](../../../../docs/standard/data/xml/resolving-external-resources-during-xslt-processing.md)  
 外部リソースを解決するための <xref:System.Xml.XmlResolver> クラスの使用について説明します。  
  
 [XSLT スタイル シートの拡張](../../../../docs/standard/data/xml/extending-xslt-style-sheets.md)  
 XSLT の拡張機能のサポートについて説明します。  
  
|||  
|-|-|  
|[XSLT エラーの解決](../../../../docs/standard/data/xml/recoverable-xslt-errors.md)|W3C (World Wide Web Consortium) 勧告『XSLT 1.0』で許可されている随意動作を示し、<xref:System.Xml.Xsl.XslCompiledTransform> クラスによるこれらの動作の処理方法を説明します。|  
|[方法 : ノード フラグメントを変換する](../../../../docs/standard/data/xml/how-to-transform-a-node-fragment.md)|ノード フラグメントの変換方法を説明します。|  
  
## <a name="related-sections"></a>関連項目  
 [XslTransform クラスからの移行](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md)  
 <xref:System.Xml.Xsl.XslTransform> クラスからコードを移行する方法について説明します。  
  
## <a name="see-also"></a>参照  
 <xref:System.Xml.Xsl.XsltSettings>  
 <xref:System.Xml.Xsl.XsltMessageEncounteredEventArgs>
