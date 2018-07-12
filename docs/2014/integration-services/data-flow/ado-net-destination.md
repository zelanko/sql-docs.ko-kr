---
title: ADO NET 대상 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.adonetdest.f1
helpviewer_keywords:
- destinations [Integration Services], ADO.NET
- ADO.NET destination
ms.assetid: cb883990-d875-4d8b-b868-45f9f15ebeae
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0233bc6dad87580764f67eea68f20171bcb5e82e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37164844"
---
# <a name="ado-net-destination"></a>ADO.NET 대상
  ADO.NET 대상은 데이터베이스 테이블이나 뷰를 사용하는 다양한 [!INCLUDE[vstecado](../../includes/vstecado-md.md)]호환 데이터베이스로 데이터를 로드합니다. 이 데이터를 기존 테이블이나 뷰에 로드하는 옵션이 제공되거나 새 테이블을 만들고 데이터를 새 테이블에 로드할 수 있습니다.  
  
 ADO NET 대상을 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에 연결할 수 있습니다. OLE DB를 사용하여 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 에 연결할 수는 없습니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 대한 자세한 내용은 [일반 보안 지침 및 제한 사항(Microsoft Azure SQL Database)](http://go.microsoft.com/fwlink/?LinkId=248228)을 참조하세요.  
  
## <a name="troubleshooting-the-ado-net-destination"></a>ADO.NET 대상 문제 해결  
 ADO.NET 대상이 외부 데이터 공급자에 대해 수행하는 호출을 로깅할 수 있습니다. 이 로깅 기능을 사용하여 ADO.NET 대상이 수행하는 외부 데이터 원본에 대한 데이터 저장 문제를 해결할 수 있습니다. ADO.NET 대상이 외부 데이터 공급자에 대해 수행하는 호출을 로깅하려면 패키지 로깅을 설정하고 패키지 수준에서 **Diagnostic** 이벤트를 선택합니다. 자세한 내용은 [패키지 실행 문제 해결 도구](../troubleshooting/troubleshooting-tools-for-package-execution.md)를 참조하세요.  
  
## <a name="configuring-the-ado-net-destination"></a>ADO.NET 대상 구성  
 이 대상은 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 사용하여 데이터 원본에 연결하며 연결 관리자에서는 사용할 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 공급자를 지정합니다. 자세한 내용은 [ADO.NET Connection Manager](../connection-manager/ado-net-connection-manager.md)를 참조하세요.  
  
 ADO.NET 대상에는 입력 열과 대상 데이터 원본 열 사이의 매핑이 포함되므로 입력 열을 모든 대상 열에 매핑하지 않아도 됩니다. 그러나 일부 대상 열의 속성에서 입력 열을 매핑해야 할 수도 있습니다. 그렇지 않으면 오류가 발생할 수 있습니다. 예를 들어 대상 열에 Null 값이 허용되지 않는 경우에는 입력 열을 해당 대상 열로 매핑해야 합니다. 또한 매핑된 열의 데이터 형식이 호환되어야 합니다. 예를 들어 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 공급자에서 지원하지 않을 경우 문자열 데이터 형식의 입력 열을 숫자 데이터 형식의 대상 열에 매핑할 수 없습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 데이터 형식이 이미지로 설정된 열에 텍스트 삽입을 지원하지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식에 대한 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)을 참조하세요.  
  
> [!NOTE]  
>  ADO.NET 대상은 DT_DBTIME 유형으로 설정된 입력 열을 datetime 유형으로 설정된 데이터베이스 열에 매핑하는 작업을 지원하지 않습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식에 대한 자세한 내용은 [Integration Services 데이터 형식](integration-services-data-types.md)을 참조하세요.  
  
 ADO.NET 대상에는 하나의 일반 입력과 하나의 오류 출력이 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **ADO.NET 대상 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [ADO NET 대상 편집기 &#40;연결 관리자 페이지&#41;](../ado-net-destination-editor-connection-manager-page.md)  
  
-   [ADO NET 대상 편집기 &#40;매핑 페이지&#41;](../ado-net-destination-editor-mappings-page.md)  
  
-   [ADO NET 대상 편집기 &#40;오류 출력 페이지&#41;](../ado-net-destination-editor-error-output-page.md)  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](../common-properties.md)  
  
-   [ADO.NET 사용자 지정 속성](ado-net-custom-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
  
