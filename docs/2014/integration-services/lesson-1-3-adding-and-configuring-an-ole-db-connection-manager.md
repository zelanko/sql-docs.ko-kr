---
title: '3단계: 추가 하 고 OLE DB 연결 관리자 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e7b74cba-a0e5-4478-af12-3f81b9484e9e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c22c9ca183a5975b762fd166ee434f305422e6ed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62891722"
---
# <a name="step-3-adding-and-configuring-an-ole-db-connection-manager"></a>3단계: 추가 하 고 OLE DB 연결 관리자 구성
  데이터 원본에 연결하기 위해 플랫 파일 연결 관리자를 추가한 후에는 OLE DB 연결 관리자를 추가하여 대상에 연결합니다. OLE DB 연결 관리자를 사용하면 패키지가 OLE DB 호환 데이터 원본에서 데이터를 추출하거나 데이터를 로드할 수 있습니다. OLE DB 연결 관리자를 사용하여 서버, 인증 방법 및 연결의 기본 데이터베이스를 지정할 수 있습니다.  
  
 이 단원에서는 Windows 인증을 사용하여 **AdventureWorksDB2012**의 로컬 인스턴스에 연결하는 OLE DB 연결 관리자를 만듭니다. 여기서 만든 OLE DB 연결 관리자는 이 자습서의 뒷부분에서 만들 다른 구성 요소(예: 조회 변환 및 OLE DB 대상)도 참조합니다.  
  
### <a name="to-add-and-configure-an-ole-db-connection-manager-to-the-ssis-package"></a>OLE DB 연결 관리자를 SSIS 패키지에 추가하고 구성하려면  
  
1.  **연결 관리자** 영역의 아무 곳이나 마우스 오른쪽 단추로 클릭한 다음 **새 OLE DB 연결**을 클릭합니다.  
  
2.  **OLE DB 연결 관리자 구성** 대화 상자에서 **새로 만들기**를 클릭합니다.  
  
3.  **서버 이름**에 **localhost**를 입력합니다.  
  
     서버 이름으로 localhost를 지정하면 연결 관리자는 로컬 컴퓨터에 있는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 기본 인스턴스에 연결합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 원격 인스턴스를 사용하려면 localhost 대신 연결하려는 서버의 이름을 입력합니다.  
  
4.  **서버에 로그온** 그룹에서 **Windows 인증 사용** 을 선택했는지 확인합니다.  
  
5.  에 **데이터베이스에 연결** 그룹에 **데이터베이스 이름 선택 또는 입력** 상자를 입력 하거나 선택 `AdventureWorksDW2012`합니다.  
  
6.  **연결 테스트** 를 클릭하여 지정한 연결 설정이 올바른지 확인합니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  **확인**을 클릭합니다.  
  
9. **OLE DB 연결 관리자 구성** 대화 상자의 **데이터 연결** 창에서 **localhost.AdventureWorksDW2012** 를 선택했는지 확인합니다.  
  
10. **확인**을 클릭합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [4단계: 패키지에 데이터 흐름 태스크 추가](lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
## <a name="see-also"></a>관련 항목  
 [OLE DB 연결 관리자](connection-manager/ole-db-connection-manager.md)  
  
  
