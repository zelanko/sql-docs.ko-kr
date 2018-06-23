---
title: ADO NET 원본 편집기 (연결 관리자 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.adonetsource.connection.f1
ms.assetid: 7de3f438-bdd6-49b5-937a-47369e754943
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9ef6c300f4954d776dc3ca6bbb5a0504c56b0c3d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093362"
---
# <a name="ado-net-source-editor-connection-manager-page"></a>ADO NET 원본 편집기(연결 관리자 페이지)
  **ADO NET 원본 편집기** 대화 상자의 **연결 관리자** 페이지를 사용하여 원본의 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 연결 관리자를 선택할 수 있습니다. 이 페이지를 사용하면 데이터베이스에서 테이블이나 뷰를 선택할 수도 있습니다.  
  
 ADO NET 원본에 대한 자세한 내용은 [ADO NET Source](data-flow/ado-net-source.md)을 참조하십시오.  
  
 **연결 관리자 페이지를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 ADO NET 원본이 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 ADO NET 원본을 두 번 클릭합니다.  
  
3.  **ADO NET 원본 편집기**에서 **연결 관리자**를 클릭합니다.  
  
## <a name="static-options"></a>정적 옵션  
 **ADO.NET 연결 관리자**  
 목록에서 기존 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 **ADO.NET 연결 관리자 구성** 대화 상자를 사용하여 새 연결 관리자를 만듭니다.  
  
 **데이터 액세스 모드**  
 원본에서 데이터를 선택하는 방법을 지정합니다.  
  
|옵션|Description|  
|------------|-----------------|  
|테이블 또는 뷰|[!INCLUDE[vstecado](../includes/vstecado-md.md)] 데이터 원본에 있는 테이블이나 뷰에서 데이터를 검색합니다.|  
|SQL 명령|SQL 쿼리를 사용하여 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 데이터 원본에서 데이터를 검색합니다.|  
  
 **미리 보기**  
 **데이터 보기** 대화 상자를 사용하여 결과를 미리 봅니다. **미리 보기** 에는 최대 200개의 행이 표시될 수 있습니다.  
  
> [!NOTE]  
>  데이터를 미리 보면 CLR 사용자 정의 형식의 열에 데이터가 포함되지 않습니다. 대신 \<값이 너무 커서 표시할 수 없습니다> 또는 System.Byte[] 값이 표시됩니다. 전자는 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 공급자를 사용하여 데이터 원본에 액세스하는 경우 표시되고 후자는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client 공급자를 사용하는 경우 표시됩니다.  
  
## <a name="data-access-mode-dynamic-options"></a>데이터 액세스 모드 동적 옵션  
  
### <a name="data-access-mode--table-or-view"></a>데이터 액세스 모드 = 테이블 또는 뷰  
 **테이블 또는 뷰 이름**  
 데이터 원본의 사용 가능한 테이블 또는 뷰 목록에서 테이블 또는 뷰 이름을 선택합니다.  
  
### <a name="data-access-mode--sql-command"></a>데이터 액세스 모드 = SQL 명령  
 **SQL 명령 텍스트**  
 SQL 쿼리 텍스트를 입력하고 **쿼리 작성**을 클릭하여 쿼리를 작성하거나 **찾아보기**를 클릭하여 쿼리 텍스트가 포함된 파일을 찾습니다.  
  
 **쿼리 작성**  
 **쿼리 작성기** 대화 상자를 사용하여 시각적으로 SQL 쿼리를 생성할 수 있습니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 SQL 쿼리 텍스트가 포함된 파일을 찾을 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADO NET 원본 편집기 &#40;열 페이지&#41;](../../2014/integration-services/ado-net-source-editor-columns-page.md)   
 [ADO NET 원본 편집기 &#40;오류 출력 페이지&#41;](../../2014/integration-services/ado-net-source-editor-error-output-page.md)   
 [ADO.NET 연결 관리자](connection-manager/ado-net-connection-manager.md)  
  
  