---
title: 개체 (XMLA) 만들기 및 변경 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 86f52c2ea61b8b62ea9bfe5ffe6b3c7b06977740
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50145148"
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
  
 사용할 합니다 [만들기](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla) 인스턴스에 주요 개체를 만드는 명령을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], 및 [Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla) 인스턴스에서 기존 주요 개체를 alter 명령입니다. 두 명령 모두 사용 하 여 실행 되는 [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) 메서드.  
  
## <a name="creating-objects"></a>개체 만들기  
 사용 하 여 개체를 만들 때 합니다 **만들기** 메서드를 먼저 식별 해야 포함 된 부모 개체를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 만들 개체입니다. 에 개체 참조를 제공 하 여 부모 개체를 식별할 수는 [ParentObject](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) 의 속성을 **만들기** 명령입니다. 각 개체 참조에 대 한 부모 개체를 고유 하 게 식별 하는 데 필요한 개체 식별자를 포함 합니다 **만들기** 명령입니다. 개체 참조에 대 한 자세한 내용은 참조 하세요. [정 및 식별 개체 &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md)합니다.  
  
 예를 들어 큐브에 대한 새 측정값 그룹을 만들려면 큐브에 대한 개체 참조를 제공해야 합니다. 큐브에 대 한 개체 참조를 **ParentObject** 를 다른 데이터베이스 에서도 동일한 큐브 식별자를 사용할 수 있으므로 속성은 데이터베이스 식별자와 큐브 식별자가 모두 포함 합니다.  
  
 합니다 [ObjectDefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla) 요소는 만들려는 주요 개체를 정의 하는 Analysis Services Scripting Language (ASSL) 요소를 포함 합니다. ASSL에 대 한 자세한 내용은 참조 하세요. [Analysis Services Scripting Language를 사용 하 여 개발 &#40;ASSL&#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)합니다.  
  
 설정 하는 경우는 **AllowOverwrite** 특성을 **만들기** 명령을 true로 지정 된 식별자를가지고 있는 기존 주요 개체를 덮어쓸 수 있습니다. true로 설정하지 않으면 지정된 식별자를 가지고 있는 주요 개체가 부모 개체에 이미 있을 경우 오류가 발생합니다.  
  
 에 대 한 자세한 내용은 합니다 **만들기** 명령을 참조 하십시오 [요소 만들기 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla).  
  
### <a name="creating-session-objects"></a>세션 개체 만들기  
 세션 개체는 클라이언트 응용 프로그램에서 사용하는 명시적 또는 암시적 세션에만 사용할 수 있는 임시 개체로, 세션이 종료될 때 삭제됩니다. 설정 하 여 세션 개체를 만들 수 있습니다 합니다 **범위** 특성을 **만들기** 명령을 *세션*합니다.  
  
> [!NOTE]  
>  사용 하는 경우는 *세션* 설정에 **ObjectDefinition** 요소만 포함할 수 있습니다 [차원](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl)를 [큐브](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl), 또는 [ MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) ASSL 요소.  
  
## <a name="altering-objects"></a>개체 변경  
 사용 하 여 개체를 수정 하는 경우는 **Alter** 메서드를 먼저 식별 해야에 개체 참조를 제공 하 여 수정할 개체를 [개체](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) 속성을 **Alter**명령입니다. 각 개체 참조에 대 한 개체를 고유 하 게 식별 하는 데 필요한 개체 식별자를 포함 합니다 **Alter** 명령입니다. 개체 참조에 대 한 자세한 내용은 참조 하세요. [정 및 식별 개체 &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md)합니다.  
  
 예를 들어 큐브의 구조를 수정하려면 큐브에 대한 개체 참조를 제공해야 합니다. 큐브에 대 한 개체 참조를 **개체** 를 다른 데이터베이스 에서도 동일한 큐브 식별자를 사용할 수 있으므로 속성은 데이터베이스 식별자와 큐브 식별자가 모두 포함 합니다.  
  
 합니다 **ObjectDefinition** 요소는 수정할 주요 개체를 정의 하는 ASSL 요소를 포함 합니다. ASSL에 대 한 자세한 내용은 참조 하세요. [Analysis Services Scripting Language를 사용 하 여 개발 &#40;ASSL&#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)합니다.  
  
 설정 하는 경우는 **AllowCreate** 특성을 **Alter** true로 명령 개체가 존재 하지 않는 경우 지정된 된 주요 개체를 만들 수 있습니다. true로 설정하지 않으면 지정된 주요 개체가 없을 경우 오류가 발생합니다.  
  
### <a name="using-the-objectexpansion-attribute"></a>ObjectExpansion 특성 사용  
 주요 개체의 속성만 변경 하 고 주요 개체에 포함 된 보조 개체를 다시 정의 하지 않은 경우 설정할 수 있습니다 합니다 **ObjectExpansion** 특성을 **Alter** 명령 *ObjectProperties*합니다. **ObjectDefinition** 속성 다음에 주요 개체의 속성에 대 한 요소를 포함 하 고 **Alter** 명령 그대로 주요 개체에 연결 된 보조 개체를 유지 합니다.  
  
 주요 개체의 보조 개체를 재정의 하려면 설정 해야 합니다 **ObjectExpansion** 특성을 *ExpandFull* 개체 정의는 주요 개체에 포함 된 모든 보조 개체가 포함 해야 합니다. 경우는 **ObjectDefinition** 의 속성을 **Alter** 명령은 주요 개체에 포함 된 보조 개체를 명시적으로 포함 되지 않습니다, 포함 되지 않은 보조 개체는 삭제 됩니다.  
  
### <a name="altering-session-objects"></a>세션 개체 변경  
 으로 만든 세션 개체를 수정 하는 **만들기** 명령으로 설정 합니다 **범위** 특성을 **Alter** 명령을 *세션*.  
  
> [!NOTE]  
>  사용 하는 경우는 *세션* 설정에 **ObjectDefinition** 요소만 포함할 수 있습니다 [차원](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl)를 [큐브](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl), 또는 [ MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) ASSL 요소.  
  
## <a name="creating-or-altering-subordinate-objects"></a>하위 개체 만들기 또는 변경  
 하지만 **Create** 또는 **Alter** 만들거나 수정 하려는 주요 개체는 묶는 내에서 정의 포함할 수 있습니다, 명령 만들거나 맨 위에 있는 주요 개체를 하나만 변경  **ObjectDefinition** 종속 된 다른 주 버전과 부 개체에 대 한 속성입니다. 예를 들어, 부모 데이터베이스에 지정 하면 큐브를 정의할 **ParentObject**, 및 큐브 정의 내에서 **ObjectDefinition** 큐브 및 측정값 내에서 측정값 그룹을 정의할 수 있습니다 그룹 각 측정값 그룹에 대 한 파티션을 정의할 수 있습니다. 보조 개체는 자신이 포함된 주요 개체 아래에만 정의될 수 있습니다. 주 및 부 개체에 대 한 자세한 내용은 참조 하세요. [데이터베이스 개체 &#40;Analysis Services-Multidimensional Data&#41;](../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)합니다.  
  
## <a name="examples"></a>예  
  
### <a name="description"></a>Description  
 다음 예제에서는 관계형 데이터 원본을 참조 하는 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 샘플 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.  
  
### <a name="code"></a>코드  
  
```  
<Create xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
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
  
### <a name="description"></a>Description  
 다음 예제에서는 이전 예제에서 만든 관계형 데이터 원본을 변경하여 데이터 원본에 대한 쿼리 제한 시간을 30초로 설정합니다.  
  
### <a name="code"></a>코드  
  
```  
<Alter ObjectExpansion="ObjectProperties" xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
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
  
### <a name="comments"></a>주석  
 **ObjectExpansion** 특성을 **Alter** 명령으로 설정 되었습니다 *ObjectProperties*합니다. 이 설정을 사용 하는 [ImpersonationInfo](https://docs.microsoft.com/bi-reference/assl/properties/impersonationinfo-element-assl) 요소에 정의 된 데이터 원본에서 제외할 개체를 부 **ObjectDefinition**합니다. 따라서 해당 데이터 원본에 대한 가장 정보가 첫 번째 예제에서 지정한 대로 서비스 계정으로 설정된 채 유지됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [메서드를 실행 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)   
 [ASSL&#40;Analysis Services Scripting Language&#41;을 사용하여 개발](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Analysis Services에서 XMLA를 사용하여 개발](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
