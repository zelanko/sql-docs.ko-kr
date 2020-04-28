---
title: 개체 만들기 및 변경 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- objects [XML for Analysis]
- subordinate objects [XML for Analysis]
- XML for Analysis, objects
- modifying objects
- removing objects
- deleting objects
- XMLA, objects
ms.assetid: a2080867-e130-440c-92eb-f768869f34a8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3dcc6eedc97b3d476d79420b4e067883e17f03d2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62702296"
---
# <a name="creating-and-altering-objects-xmla"></a>개체 만들기 및 변경(XMLA)
  주요 개체는 독립적으로 만들고 변경하고 삭제할 수 있습니다. 주요 개체에는 다음과 같은 개체가 포함됩니다.  
  
-   서버  
  
-   데이터베이스  
  
-   차원  
  
-   큐브  
  
-   측정값 그룹  
  
-   파티션  
  
-   큐브 뷰  
  
-   마이닝 모델  
  
-   역할  
  
-   서버 또는 데이터베이스에 연결된 명령  
  
-   데이터 원본  
  
 [Create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla) 명령을 사용 하면 인스턴스에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]주요 개체를 만들고 [alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla) 명령을 사용 하 여 인스턴스의 기존 주요 개체를 변경할 수 있습니다. 두 명령은 모두 [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) 메서드를 사용 하 여 실행 됩니다.  
  
## <a name="creating-objects"></a>개체 만들기  
 `Create` 메서드를 사용하여 개체를 만들려면 먼저 만들려는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체가 포함된 부모 개체를 식별해야 하는데, `Create` 명령의 [parentobject](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) 속성에 개체 참조를 제공 하 여 부모 개체를 식별할 수 있습니다. 각 개체 참조에는 `Create` 명령에 대한 부모 개체를 고유하게 식별하는 데 필요한 개체 식별자가 들어 있습니다. 개체 참조에 대 한 자세한 내용은 [XMLA&#41;&#40;개체 정의 및 식별 ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)을 참조 하세요.  
  
 예를 들어 큐브에 대한 새 측정값 그룹을 만들려면 큐브에 대한 개체 참조를 제공해야 합니다. 동일한 큐브 식별자를 다른 데이터베이스에서도 사용할 수 있으므로 `ParentObject` 속성의 큐브에 대한 개체 참조에는 데이터베이스 식별자와 큐브 식별자가 모두 들어 있습니다.  
  
 [Objectdefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla) 요소는 만들려는 주요 개체를 정의 하는 개체 (Analysis Services Scripting Language) 요소를 포함 합니다. 을 사용 하는 방법에 대 한 자세한 내용은 [Analysis Services 스크립팅 언어 &#40;를 사용 하 여 개발&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)을 참조 하십시오.  
  
 `AllowOverwrite` 명령의 `Create` 특성을 true로 설정하면 지정된 식별자를 가지고 있는 기존 주요 개체를 덮어쓸 수 있습니다. true로 설정하지 않으면 지정된 식별자를 가지고 있는 주요 개체가 부모 개체에 이미 있을 경우 오류가 발생합니다.  
  
 `Create` 명령에 대 한 자세한 내용은 [CREATE Element &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)를 참조 하세요.  
  
### <a name="creating-session-objects"></a>세션 개체 만들기  
 세션 개체는 클라이언트 애플리케이션에서 사용하는 명시적 또는 암시적 세션에만 사용할 수 있는 임시 개체로, 세션이 종료될 때 삭제됩니다. 명령의 특성을 Session으로 설정 하 여 세션 개체를 만들 수 있습니다. *Session* `Scope` `Create`  
  
> [!NOTE]  
>  *Session* 설정을 사용 하는 경우 요소 `ObjectDefinition` 는 [Dimension](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl), [Cube](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl)또는 [MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) vall 요소만 포함할 수 있습니다.  
  
## <a name="altering-objects"></a>개체 변경  
 메서드를 사용 하 여 개체를 수정 하는 경우 먼저 `Alter` 명령의 [object](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) 속성에 개체 참조를 제공 하 여 수정할 개체를 식별 해야 합니다. `Alter` 각 개체 참조에는 `Alter` 명령에 대한 개체를 고유하게 식별하는 데 필요한 개체 식별자가 들어 있습니다. 개체 참조에 대 한 자세한 내용은 [XMLA&#41;&#40;개체 정의 및 식별 ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)을 참조 하세요.  
  
 예를 들어 큐브의 구조를 수정하려면 큐브에 대한 개체 참조를 제공해야 합니다. 동일한 큐브 식별자를 다른 데이터베이스에서도 사용할 수 있으므로 `Object` 속성의 큐브에 대한 개체 참조에는 데이터베이스 식별자와 큐브 식별자가 모두 들어 있습니다.  
  
 `ObjectDefinition` 요소는 수정할 주요 개체를 정의하는 ASSL 요소를 포함합니다. 을 사용 하는 방법에 대 한 자세한 내용은 [Analysis Services 스크립팅 언어 &#40;를 사용 하 여 개발&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)을 참조 하십시오.  
  
 `AllowCreate` 명령의 `Alter` 특성을 true로 설정하면 지정된 주요 개체가 없는 경우 해당 개체를 만들 수 있습니다. true로 설정하지 않으면 지정된 주요 개체가 없을 경우 오류가 발생합니다.  
  
### <a name="using-the-objectexpansion-attribute"></a>ObjectExpansion 특성 사용  
 주요 개체의 속성만 변경 하 고 주요 개체에 포함 된 보조 개체를 다시 정의 하지 않는 경우 `ObjectExpansion` `Alter` 명령의 특성을 *objectproperties*로 설정할 수 있습니다. 이 경우 `ObjectDefinition` 속성은 주요 개체의 속성에 대한 요소만 포함해야 하며 `Alter` 명령은 주요 개체에 연결된 보조 개체를 그대로 유지합니다.  
  
 주요 개체의 보조 개체를 다시 정의 하려면 `ObjectExpansion` 특성을 *updateoptions.expandfull* 로 설정 해야 하며, 개체 정의에는 주요 개체에 포함 된 모든 보조 개체가 포함 되어야 합니다. 주요 개체에 포함된 보조 개체가 `ObjectDefinition` 명령의 `Alter` 속성에 명시적으로 포함되지 않은 경우 포함되지 않은 보조 개체는 삭제됩니다.  
  
### <a name="altering-session-objects"></a>세션 개체 변경  
 `Create` 명령으로 만든 세션 개체를 수정 하려면 `Scope` `Alter` 명령의 특성을 *session*으로 설정 합니다.  
  
> [!NOTE]  
>  *Session* 설정을 사용 하는 경우 요소 `ObjectDefinition` 는 [Dimension](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl), [Cube](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl)또는 [MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) vall 요소만 포함할 수 있습니다.  
  
## <a name="creating-or-altering-subordinate-objects"></a>하위 개체 만들기 또는 변경  
 `Create` 또는 `Alter` 명령으로는 최상위의 주요 개체를 한 개만 만들거나 변경할 수 있지만 만들거나 수정하려는 주요 개체는 묶는 `ObjectDefinition` 속성 내에 다른 주요 개체 및 해당 주요 개체에 종속된 보조 개체에 대한 정의를 포함할 수 있습니다. 예를 들어 큐브를 정의하고 `ParentObject`에 부모 데이터베이스를 지정한 경우 `ObjectDefinition`의 큐브 정의 내에서는 큐브에 대한 측정값 그룹을 정의할 수 있으며, 이 측정값 그룹 내에서는 각 측정값 그룹에 대한 파티션을 정의할 수 있습니다. 보조 개체는 자신이 포함된 주요 개체 아래에만 정의될 수 있습니다. 주 개체 및 보조 개체에 대 한 자세한 내용은 [데이터베이스 개체 &#40;Analysis Services-다차원 데이터&#41;](../multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)를 참조 하세요.  
  
## <a name="examples"></a>예  
  
### <a name="description"></a>설명  
 다음 예에서는 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 예제 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 참조 하는 관계형 데이터 원본을 만듭니다.  
  
### <a name="code"></a>코드  
  
```  
<Create xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <ParentObject>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    </ParentObject>  
    <ObjectDefinition>  
        <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RelationalDataSource">  
            <ID>AdventureWorksDW2012</ID>  
            <Name>AdventureWorksDW2012</Name>  
            <ConnectionString>Data Source=localhost;Initial Catalog=AdventureWorksDW2008R2;Integrated Security=True</ConnectionString>  
            <ImpersonationInfo>  
                <ImpersonationMode>ImpersonateServiceAccount</ImpersonationMode>  
            </ImpersonationInfo>  
            <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
            <Timeout>PT0S</Timeout>  
        </DataSource>  
    </ObjectDefinition>  
</Create>  
```  
  
### <a name="description"></a>설명  
 다음 예제에서는 이전 예제에서 만든 관계형 데이터 원본을 변경하여 데이터 원본에 대한 쿼리 제한 시간을 30초로 설정합니다.  
  
### <a name="code"></a>코드  
  
```  
<Alter ObjectExpansion="ObjectProperties" xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <DataSourceID>AdventureWorksDW2012</DataSourceID>  
    </Object>  
    <ObjectDefinition>  
        <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RelationalDataSource">  
            <ID>AdventureWorksDW2012</ID>  
            <Name>AdventureWorksDW2012</Name>  
            <ConnectionString>Data Source=fr-dwk-02;Initial Catalog=AdventureWorksDW2008R2;Integrated Security=True</ConnectionString>  
            <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
            <Timeout>PT30S</Timeout>  
        </DataSource>  
    </ObjectDefinition>  
</Alter>  
```  
  
### <a name="comments"></a>설명  
 `Alter` 명령의 `ObjectExpansion` 특성이 *objectproperties*로 설정 되었습니다. 이 설정을 사용 하면 보조 개체인 [ImpersonationInfo](https://docs.microsoft.com/bi-reference/assl/properties/impersonationinfo-element-assl) 요소를에 `ObjectDefinition`정의 된 데이터 원본에서 제외할 수 있습니다. 따라서 해당 데이터 원본에 대한 가장 정보가 첫 번째 예제에서 지정한 대로 서비스 계정으로 설정된 채 유지됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [XMLA&#41;&#40;메서드를 실행 합니다.](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)   
 [Analysis Services 스크립팅 언어 &#40;를 사용 하 여 개발&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Analysis Services에서 XMLA를 사용하여 개발](developing-with-xmla-in-analysis-services.md)  
  
  
