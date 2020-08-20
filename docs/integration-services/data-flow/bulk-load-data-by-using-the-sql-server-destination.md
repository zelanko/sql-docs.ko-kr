---
description: SQL Server 대상을 사용하여 데이터 대량 로드
title: SQL Server 대상을 사용하여 데이터 대량 로드 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server destination
- loading data
- destinations [Integration Services], SQL Server
- inserting data
- bulk load [Integration Services]
ms.assetid: 8f982f85-a82e-4e2d-9cd8-cd2f85402d8e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3bce4cae8fc71c93487f65a726bb42f58618d5a7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457451"
---
# <a name="bulk-load-data-by-using-the-sql-server-destination"></a>SQL Server 대상을 사용하여 데이터 대량 로드

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상을 추가 및 구성하려면 패키지에 적어도 하나 이상의 데이터 흐름 태스크와 하나의 데이터 원본이 이미 들어 있어야 합니다.  
  
### <a name="to-load-data-using-a-sql-server-destination"></a>SQL Server 대상을 사용하여 데이터를 로드하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **데이터 흐름** 탭을 클릭한 다음 **도구 상자**에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상을 디자인 화면으로 끌어 옵니다.  
  
4.  연결선을 대상으로 끌어 와서 대상을 데이터 흐름에 있는 원본 또는 이전 변환에 연결합니다.  
  
5.  대상을 두 번 클릭합니다.  
  
6.  **SQL Server 대상 편집기**의 **연결 관리자** 페이지에서 기존 OLE DB 연결 관리자를 선택하거나 **새로 만들기** 를 클릭하여 새 연결 관리자를 만듭니다. 자세한 내용은 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)를 참조하세요.  
  
7.  데이터를 로드할 테이블 또는 뷰를 지정하려면 다음 중 하나를 수행하십시오.  
  
    -   기존 테이블 또는 뷰를 선택합니다.  
  
    -   **새로 만들기**를 클릭하고 **테이블 만들기** 대화 상자에서 테이블 또는 뷰를 만드는 SQL 문을 작성합니다.  
  
        > [!NOTE]  
        >  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 연결된 데이터 원본에 따라 기본 CREATE TABLE 문을 생성합니다. 원본 테이블에 선언된 FILESTREAM 특성이 포함된 열이 있어도 기본 CREATE TABLE 문은 FILESTREAM 특성을 포함하지 않습니다. FILESTREAM 특성이 포함된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소를 실행하려면 먼저 대상 데이터베이스에서 FILESTREAM 스토리지를 구현하십시오. 그런 다음 **테이블 만들기** 대화 상자에서 FILESTREAM 특성을 CREATE TABLE 문에 추가하십시오. 자세한 내용은 [Blob&#40;Binary Large Object&#41; 데이터&#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)를 참조하세요.  
  
8.  **매핑** 을 클릭하고 **사용 가능한 입력 열** 목록의 열을 **사용 가능한 대상 열** 목록의 열로 끌어서 매핑합니다.  
  
    > [!NOTE]  
    >  대상은 같은 이름의 열로 자동으로 매핑됩니다.  
  
9. **고급** 을 클릭하고 **ID 유지**, **Null 유지**, **테이블 잠금**, **CHECK 제약 조건**및 **트리거 실행**과 같은 대량 로드 옵션을 설정합니다.  
  
     선택적으로 삽입할 첫 번째와 마지막 입력 행, 삽입 작업이 중지되기 전에 발생할 수 있는 최대 오류 개수 및 삽입이 정렬될 열을 지정합니다.  
  
    > [!NOTE]  
    >  정렬 순서는 열이 나열되는 순서에 따라 결정됩니다.  
  
10. **확인**을 클릭합니다.  
  
11. 업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Destination](../../integration-services/data-flow/sql-server-destination.md)   
 [Integration Services 변환](../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services 경로](../../integration-services/data-flow/integration-services-paths.md)   
 [데이터 흐름 태스크](../../integration-services/control-flow/data-flow-task.md)  
  
  
