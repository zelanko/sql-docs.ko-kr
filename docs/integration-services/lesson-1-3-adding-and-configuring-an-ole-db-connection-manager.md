---
title: "3단계: OLE DB 연결 관리자 추가 및 구성 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: e7b74cba-a0e5-4478-af12-3f81b9484e9e
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 86d3e42b79efd2f2541c575b2c860b0a5cb4f41b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="lesson-1-3---adding-and-configuring-an-ole-db-connection-manager"></a>1-3단원: OLE DB 연결 관리자 추가 및 구성
데이터 원본에 연결하기 위해 플랫 파일 연결 관리자를 추가한 후에는 OLE DB 연결 관리자를 추가하여 대상에 연결합니다. OLE DB 연결 관리자를 사용하면 패키지가 OLE DB 호환 데이터 원본에서 데이터를 추출하거나 데이터를 로드할 수 있습니다. OLE DB 연결 관리자를 사용하여 서버, 인증 방법 및 연결의 기본 데이터베이스를 지정할 수 있습니다.  
  
이 단원에서는 Windows 인증을 사용하여 **AdventureWorksDB2012**의 로컬 인스턴스에 연결하는 OLE DB 연결 관리자를 만듭니다. 여기서 만든 OLE DB 연결 관리자는 이 자습서의 뒷부분에서 만들 다른 구성 요소(예: 조회 변환 및 OLE DB 대상)도 참조합니다.  
  
### <a name="add-and-configure-an-ole-db-connection-manager-to-the-ssis-package"></a>SSIS 패키지에 OLE DB 연결 관리자 추가 및 구성  
  
1.  **연결 관리자** 영역의 아무 곳이나 마우스 오른쪽 단추로 클릭한 다음 **새 OLE DB 연결**을 클릭합니다.  
  
2.  **OLE DB 연결 관리자 구성** 대화 상자에서 **새로 만들기**를 클릭합니다.  
  
3.  **서버 이름**에 **localhost**를 입력합니다.  
  
    서버 이름으로 localhost를 지정하면 연결 관리자는 로컬 컴퓨터에 있는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 기본 인스턴스에 연결합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 원격 인스턴스를 사용하려면 localhost 대신 연결하려는 서버의 이름을 입력합니다.  
  
4.  **서버에 로그온** 그룹에서 **Windows 인증 사용** 을 선택했는지 확인합니다.  
  
5.  **데이터베이스에 연결** 그룹의 **데이터베이스 이름 선택 또는 입력** 상자에 **AdventureWorksDW2012**를 입력하거나 선택합니다.  
  
6.  **연결 테스트** 를 클릭하여 지정한 연결 설정이 올바른지 확인합니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  **확인**을 클릭합니다.  
  
9. **OLE DB 연결 관리자 구성** 대화 상자의 **데이터 연결** 창에서 **localhost.AdventureWorksDW2012** 를 선택했는지 확인합니다.  
  
10. **확인**을 클릭합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[4단계: 패키지에 데이터 흐름 태스크 추가](../integration-services/lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
## <a name="see-also"></a>참고 항목  
[OLE DB 연결 관리자](../integration-services/connection-manager/ole-db-connection-manager.md)  
  
