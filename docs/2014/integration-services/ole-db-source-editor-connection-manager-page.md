---
title: OLE DB 원본 편집기 (연결 관리자 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbsourceadapter.connection.f1
helpviewer_keywords:
- OLE DB Source Editor
ms.assetid: 53699902-8699-4547-b56b-a5b2079e98b6
caps.latest.revision: 41
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 71b29c69425508e15ba306c6f9ae7d0319c8a6ca
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37206493"
---
# <a name="ole-db-source-editor-connection-manager-page"></a>OLE DB 원본 편집기(연결 관리자 페이지)
  **OLE DB 원본 편집기** 대화 상자의 **연결 관리자** 페이지를 사용하여 원본의 OLE DB 연결 관리자를 선택할 수 있습니다. 이 페이지를 사용하면 데이터베이스에서 테이블이나 뷰를 선택할 수도 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel 2007을 사용하는 데이터 원본에서 데이터를 로드하려면 OLE DB 원본을 사용하십시오. Excel 원본을 사용하여 Excel 2007 데이터 원본에서 데이터를 로드할 수 없습니다. 자세한 내용은 [Configure OLE DB Connection Manager](configure-ole-db-connection-manager.md)을(를) 참조하세요.  
>   
>  [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel 2003 이전 버전을 사용하는 데이터 원본에서 데이터를 로드하려면 Excel 원본을 사용하십시오. 자세한 내용은 [Excel 원본 편집기&#40;연결 관리자 페이지&#41;](../../2014/integration-services/excel-source-editor-connection-manager-page.md)를 참조하세요.  
  
> [!NOTE]  
>  `CommandTimeout` OLE DB 원본의 속성을 사용할 수 없습니다는 **OLE DB 원본 편집기**를 사용 하 여 설정할 수 있습니다를 **고급 편집기**합니다. 이 속성에 대한 자세한 내용은 [OLE DB Custom Properties](data-flow/ole-db-custom-properties.md)의 Excel 원본 섹션을 참조하십시오.  
  
 OLE DB 원본에 대한 자세한 내용은 [OLE DB Source](data-flow/ole-db-source.md)을 참조하십시오.  
  
## <a name="open-the-ole-db-source-editor-connection-manager-page"></a>OLE DB 원본 편집기 열기(연결 관리자 페이지)  
  
1.  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 OLE DB 원본을 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에 추가합니다.  
  
2.  원본 구성 요소를 마우스 오른쪽 단추로 클릭한 다음 **편집**을 클릭합니다.  
  
3.  **연결 관리자**를 클릭합니다.  
  
## <a name="static-options"></a>정적 옵션  
 **캐시 없음**  
 목록에서 기존 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 **OLE DB 연결 관리자 구성** 대화 상자를 사용하여 새 연결 관리자를 만듭니다.  
  
 **데이터 액세스 모드**  
 원본에서 데이터를 선택하는 방법을 지정합니다.  
  
|옵션|Description|  
|------------|-----------------|  
|테이블 또는 뷰|OLE DB 데이터 원본에 있는 테이블이나 뷰에서 데이터를 검색합니다.|  
|테이블 이름 또는 뷰 이름 변수|변수에 테이블 또는 뷰 이름을 지정합니다.<br /><br /> **관련 정보:** [패키지에서 변수 사용](../../2014/integration-services/use-variables-in-packages.md)|  
|SQL 명령|SQL 쿼리를 사용하여 OLE DB 데이터 원본에서 데이터를 검색합니다.|  
|변수를 사용한 SQL 명령|변수에 SQL 쿼리 텍스트를 지정합니다.|  
  
 **미리 보기**  
 **데이터 보기** 대화 상자를 사용하여 결과를 미리 봅니다. **미리 보기** 에는 최대 200개의 행이 표시될 수 있습니다.  
  
> [!NOTE]  
>  데이터를 미리 보면 CLR 사용자 정의 형식의 열에 데이터가 포함되지 않습니다. 대신 \<값이 너무 커서 표시할 수 없습니다> 또는 System.Byte[] 값이 표시됩니다. 전자는 SQL OLE DB 공급자를 사용하여 데이터 원본에 액세스하는 경우 표시되고 후자는 &lt; [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client 공급자를 사용하는 경우 표시됩니다.  
  
## <a name="data-access-mode-dynamic-options"></a>데이터 액세스 모드 동적 옵션  
  
### <a name="data-access-mode--table-or-view"></a>데이터 액세스 모드 = 테이블 또는 뷰  
 **테이블 또는 뷰 이름**  
 데이터 원본의 사용 가능한 테이블 또는 뷰 목록에서 테이블 또는 뷰 이름을 선택합니다.  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>데이터 액세스 모드 = 테이블 이름 또는 뷰 이름 변수  
 **변수 이름**  
 테이블 또는 뷰 이름이 포함된 변수를 선택합니다.  
  
### <a name="data-access-mode--sql-command"></a>데이터 액세스 모드 = SQL 명령  
 **SQL 명령 텍스트**  
 SQL 쿼리 텍스트를 입력하고 **쿼리 작성**을 클릭하여 쿼리를 작성하거나 **찾아보기**를 클릭하여 쿼리 텍스트가 포함된 파일을 찾습니다.  
  
 **매개 변수**  
 쿼리 텍스트에 ?를 매개 변수 자리 표시자로 사용하여 매개 변수가 있는 쿼리를 입력한 경우 **쿼리 매개 변수 설정** 대화 상자를 사용하여 쿼리 입력 매개 변수를 패키지 변수에 매핑합니다.  
  
 **Build query**  
 **쿼리 작성기** 대화 상자를 사용하여 시각적으로 SQL 쿼리를 생성할 수 있습니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 SQL 쿼리 텍스트가 포함된 파일을 찾을 수 있습니다.  
  
 **쿼리 구문 분석**  
 쿼리 텍스트의 구문을 확인합니다.  
  
### <a name="data-access-mode--sql-command-from-variable"></a>데이터 액세스 모드 = 변수를 사용한 SQL 명령  
 **변수 이름**  
 SQL 쿼리 텍스트가 포함된 변수를 선택합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [OLE DB 원본 편집기 &#40;열 페이지&#41;](../../2014/integration-services/ole-db-source-editor-columns-page.md)   
 [OLE DB 원본 편집기 &#40;오류 출력 페이지&#41;](../../2014/integration-services/ole-db-source-editor-error-output-page.md)   
 [OLE DB 원본을 사용 하 여 데이터 추출](data-flow/extract-data-by-using-the-ole-db-source.md)   
 [OLE DB 연결 관리자](connection-manager/ole-db-connection-manager.md)  
  
  
