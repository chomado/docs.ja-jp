---
title: 依存関係プロパティのコールバックと検証
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- dependency properties [WPF], validation
- coerce value callbacks [WPF]
- callbacks [WPF], validation
- dependency properties [WPF], callbacks
- validation of dependency properties [WPF]
ms.assetid: 48db5fb2-da7f-49a6-8e81-3540e7b25825
ms.openlocfilehash: e181c2d9610619587642f982959f809b96b011dc
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33541334"
---
# <a name="dependency-property-callbacks-and-validation"></a>依存関係プロパティのコールバックと検証
このトピックでは、検証による判定、プロパティの有効値が変更されたときに呼び出されるコールバック、値の決定への外部的影響のオーバーライドなど、プロパティ関連機能の代替カスタム実装を使用して依存関係プロパティを作成する方法について説明します。 また、これらの手法を用いてプロパティ システムの既定の動作を拡張することが適切であるシナリオについても説明します。  
  
  
  
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>必須コンポーネント  
 このトピックでは、依存関係プロパティの実装の基本シナリオとカスタム依存関係プロパティへのメタデータの適用方法を理解していることを前提とします。 詳細については、「[カスタム依存関係プロパティ](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)」および「[依存関係プロパティのメタデータ](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md)」を参照してください。  
  
<a name="Validation_Callbacks"></a>   
## <a name="validation-callbacks"></a>検証コールバック  
 検証コールバックは、最初の登録時に依存関係プロパティに割り当てることができます。 検証コールバックは、プロパティのメタデータの一部ではありません。直接入力は、<xref:System.Windows.DependencyProperty.Register%2A>メソッドです。 したがって、依存関係プロパティの検証コールバックを作成した後で、その検証コールバックを新しい実装でオーバーライドすることはできません。  
  
 [!code-csharp[DPCallbackOverride#CurrentDefinitionWithWrapper](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DPCallbackOverride/CSharp/SDKSampleLibrary/class1.cs#currentdefinitionwithwrapper)]
 [!code-vb[DPCallbackOverride#CurrentDefinitionWithWrapper](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DPCallbackOverride/visualbasic/sdksamplelibrary/class1.vb#currentdefinitionwithwrapper)]  
  
 検証コールバックは、オブジェクト値を受け取るように実装されます。 指定された値がプロパティに対して有効である場合は `true` を、有効でない場合は `false`を返します。 プロパティの型はプロパティ システムに登録済みの適切な型であると想定されます。したがって、通常の場合、コールバック内での型チェックは行われません。 検証コールバックは、プロパティ システムが実行するさまざまな操作で使用されます。 呼び出すことによって、既定値で初期の型の初期化、プログラムによる変更が含まれます<xref:System.Windows.DependencyObject.SetValue%2A>、または指定された既定値は新しいメタデータをオーバーライドしようとします。 これらの操作で呼び出された検証コールバックが `false` を返す場合、例外が発生します。 アプリケーションの作成者はこれらの例外を処理する必要があります。 検証コールバックは、列挙値の検証や、プロパティの測定値がゼロ以上に設定されている場合に integer 型または double 型の値を制限するときによく使用されます。  
  
 検証コールバックは、インスタンスではなくクラスを検証するためのものです。 コールバックのパラメーターは、特定の通信しない<xref:System.Windows.DependencyObject>を検証するプロパティが設定されています。 したがって、検証コールバックを使用して、プロパティ値に影響を及ぼす可能性がある "依存関係" (インスタンス固有のプロパティ値が他のインスタンス固有のプロパティ値や実行時の状態などの要因に依存する関係) を強制することはできません。  
  
 非常に単純な検証コールバックを行うのためのサンプル コードを次に示します: することを検証として型指定されたプロパティ、<xref:System.Double>プリミティブは<xref:System.Double.PositiveInfinity>または<xref:System.Double.NegativeInfinity>です。  
  
 [!code-csharp[DPCallbackOverride#ValidateValueCallback](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DPCallbackOverride/CSharp/SDKSampleLibrary/class1.cs#validatevaluecallback)]
 [!code-vb[DPCallbackOverride#ValidateValueCallback](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DPCallbackOverride/visualbasic/sdksamplelibrary/class1.vb#validatevaluecallback)]  
  
<a name="Coerce_Value_Callbacks_and_Property_Changed_Events"></a>   
## <a name="coerce-value-callbacks-and-property-changed-events"></a>強制値コールバックとプロパティ変更イベント  
 強制値コールバックは、特定<xref:System.Windows.DependencyObject>プロパティの場合は、インスタンス<xref:System.Windows.PropertyChangedCallback>依存関係プロパティの値が変更されるたびに、プロパティのシステムによって呼び出される実装します。 これら 2 つのコールバックを組み合わせて使用すると、あるプロパティが変更されたときに他のプロパティに自動的に強制または再評価が適用される一連のプロパティを要素に作成することができます。  
  
 依存関係プロパティ間の関連は、最小値、最大値、および実際の値 (または現在の値) を表す 3 つ目のプロパティが要素に含まれる場合において、ユーザー インターフェイスによって駆動されるプロパティがあるときによく使用されます。 ここで、最大値が現在の値より小さい値に調整された場合、現在の値を新しい最大値以下の値に強制する必要があります。現在の値と最小値についても同様の関係が成り立ちます。  
  
 次の、3 つの依存関係プロパティの 1 つを示す非常に簡単なコード例は、こうした関係を表しています。 この例は、関連する *Reading プロパティ (Min、Max、Current) のうちの 1 つである `CurrentReading` プロパティの登録方法を示しています。 ここでは、前のセクションで説明した検証を使用しています。  
  
 [!code-csharp[DPCallbackOverride#CurrentDefinitionWithWrapper](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DPCallbackOverride/CSharp/SDKSampleLibrary/class1.cs#currentdefinitionwithwrapper)]
 [!code-vb[DPCallbackOverride#CurrentDefinitionWithWrapper](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DPCallbackOverride/visualbasic/sdksamplelibrary/class1.vb#currentdefinitionwithwrapper)]  
  
 Current のプロパティ変更コールバックを使用して、他の依存関係プロパティに対して登録されている強制値コールバックを明示的に呼び出すことにより、変更を他のプロパティに伝播します。  
  
 [!code-csharp[DPCallbackOverride#OnPCCurrent](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DPCallbackOverride/CSharp/SDKSampleLibrary/class1.cs#onpccurrent)]
 [!code-vb[DPCallbackOverride#OnPCCurrent](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DPCallbackOverride/visualbasic/sdksamplelibrary/class1.vb#onpccurrent)]  
  
 強制値コールバックは、Current プロパティが依存している可能性があるプロパティの値を検証し、必要に応じて現在の値を強制的に指定します。  
  
 [!code-csharp[DPCallbackOverride#CoerceCurrent](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DPCallbackOverride/CSharp/SDKSampleLibrary/class1.cs#coercecurrent)]
 [!code-vb[DPCallbackOverride#CoerceCurrent](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DPCallbackOverride/visualbasic/sdksamplelibrary/class1.vb#coercecurrent)]  
  
> [!NOTE]
>  プロパティの既定値は強制的に指定されません。 プロパティの値がまだ初期の既定値または経由で他の値をクリアするプロパティの値は既定値が発生する<xref:System.Windows.DependencyObject.ClearValue%2A>です。  
  
 強制値コールバックとプロパティ変更コールバックはプロパティ メタデータの一部です。 したがって、特定の依存関係プロパティを所有する型から派生させた型に存在するその特定の依存関係プロパティのコールバックは、派生させた型でプロパティのメタデータをオーバーライドすることで変更できます。  
  
<a name="Advanced"></a>   
## <a name="advanced-coercion-and-callback-scenarios"></a>高度な強制とコールバック シナリオ  
  
### <a name="constraints-and-desired-values"></a>制約と目的の値  
 <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A>コールバック プロパティ システムで宣言すると、ロジックがローカルで設定の強制変換された値に従って値を強制的に使用されるプロパティは「必要な値」を内部的に保持もします。 制約がアプリケーションの有効期間内に動的に変更される可能性があるプロパティ値に基づいている場合、強制の制約も動的に変更されます。そして、制約されているプロパティは、指定された新しい制約の下で、その値を目的の値にできる限り近づけることができます。 制約がすべて解除された場合、値は目的の値になります。 相互に循環的に依存する複数のプロパティを使用している場合、非常に複雑な依存関係シナリオを導入することができます。 たとえば、Min、Max、Current のシナリオでは、Minimum と Maximum をユーザー設定可能なプロパティにすることができます。 その場合、Maximum が常に Minimum より大きくなり、Minimum が常に Maximum より小さくなるように強制する必要があります。 ただし、この強制を有効にし、Maximum が Minimum に強制された場合、Current が未設定の状態になります。なぜなら、Currenct は Maximum と Minimum の両方に依存し、両者の値の間の範囲内 (この場合はゼロ) に制約されるからです。 その後、Maximum または Minimum が調整された場合、Current はいずれかの値を "追跡" すると考えられます。なぜなら、Current の目的の値が依然として保持されており、制約が緩和されると Current が目的の値に到達しようとするからです。  
  
 依存関係が複雑でも技術的には問題はありません。ただし、多数の再評価が必要になる場合、パフォーマンスが若干低下することがあります。また、UI に直接影響する場合は、ユーザーの混乱につながることもあります。 プロパティ変更コールバックおよび強制値コールバックについては注意が必要です。試行中の強制ができる限り明確に処理されること、およびその制約が "過剰制約" ではないことを確認してください。  
  
### <a name="using-coercevalue-to-cancel-value-changes"></a>CoerceValue を使用した値変更の取り消し  
 プロパティ システムには、いずれかの処理は<xref:System.Windows.CoerceValueCallback>値を返す<xref:System.Windows.DependencyProperty.UnsetValue>特殊なケースとして。 この特殊なケースを意味するプロパティの変更を発生させた、<xref:System.Windows.CoerceValueCallback>プロパティ システムによって拒否される必要があります呼び出されていること、およびプロパティ システムでは、プロパティがどのような以前の値を報告する代わりにします。 このメカニズムは、非同期に開始されたプロパティの変更が現在のオブジェクトの状態に対して依然として有効であるかどうかをチェックし、有効でない場合はその変更を抑制する場合に役立ちます。 考えられるもう 1 つのシナリオとして、プロパティ値の決定におけるどの構成要素が報告されるプロパティ値を決定するかに応じて値を選択的に抑制することもできます。 これを行うには、使用することができます、<xref:System.Windows.DependencyProperty>として渡されたコールバックおよびプロパティの識別子の入力を<xref:System.Windows.DependencyPropertyHelper.GetValueSource%2A>、し、処理、<xref:System.Windows.ValueSource>です。  
  
## <a name="see-also"></a>関連項目  
 [依存関係プロパティの概要](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)  
 [依存関係プロパティのメタデータ](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md)  
 [カスタム依存関係プロパティ](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)
