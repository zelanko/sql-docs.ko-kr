---
title: '3단계: OLE DB 연결 관리자 추가 및 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: e7b74cba-a0e5-4478-af12-3f81b9484e9e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f014affc4ce58243ab629c3bbf12b607d6b7954f
ms.sourcegitcommit: dd794633466b1da8ead9889f5e633bdf4b3389cd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54143513"
---
# <a name="lesson-1-3-add-and-configure-an-ole-db-connection-manager"></a>1-3단원: OLE DB 연결 관리자 추가 및 구성

데이터 원본에 연결하기 위해 플랫 파일 연결 관리자를 추가한 후에 OLE DB 연결 관리자를 추가하여 대상에 연결합니다. OLE DB 연결 관리자를 사용하면 패키지가 OLE DB 호환 데이터 원본에서 데이터를 추출하거나 데이터를 로드할 수 있습니다. OLE DB 연결 관리자를 사용하여 서버, 인증 방법 및 연결의 기본 데이터베이스를 지정할 수 있습니다.  
  
이 태스크에서는 Windows 인증을 사용하여 **AdventureWorksDW2012**의 로컬 인스턴스에 연결하는 OLE DB 연결 관리자를 만듭니다. 이 OLE DB 연결 관리자는 조회 변환 및 OLE DB 대상과 같은 이 자습서의 뒷부분에서 만드는 다른 구성 요소에서도 참조합니다.  
  
## <a name="add-and-configure-an-ole-db-connection-manager"></a>OLE DB 연결 관리자 추가 및 구성

1. **솔루션 탐색기** 창에서 **연결 관리자**를 마우스 오른쪽 단추로 클릭하고 **새 연결 관리자**를 선택합니다.

1. **SSIS 연결 관리자 추가** 대화 상자에서 **OLEDB**를 선택한 다음, **추가**를 선택합니다.
    
2. **OLE DB 연결 관리자 구성** 대화 상자에서 **새로 만들기**를 선택합니다.  
  
3. **서버 이름**에 **localhost**를 입력합니다.  
  
    서버 이름으로 localhost를 지정하면 연결 관리자는 로컬 컴퓨터에 있는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 기본 인스턴스에 연결합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 원격 인스턴스를 사용하려면 localhost 대신 연결하려는 서버의 이름을 입력합니다.  
  
4. **서버에 로그온** 그룹에서 **Windows 인증 사용** 을 선택했는지 확인합니다.  
  
5. **데이터베이스에 연결** 그룹의 **데이터베이스 이름 선택 또는 입력** 상자에 **AdventureWorksDW2012**를 입력하거나 선택합니다.  
  
6. **연결 테스트**를 선택하여 지정한 연결 설정이 올바른지 확인합니다.  
  
7. **확인**을 선택합니다.  
  
8. **확인**을 선택합니다.  
  
9. **연결 관리자** 창에서 **localhost.AdventureWorksDW2012**가 선택되어 있는지 확인합니다.  
  

## <a name="go-to-next-task"></a>다음 작업으로 이동
[4단계: 패키지에 데이터 흐름 태스크 추가](../integration-services/lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
## <a name="see-also"></a>관련 항목:  
[캐시 없음](../integration-services/connection-manager/ole-db-connection-manager.md)  
  
