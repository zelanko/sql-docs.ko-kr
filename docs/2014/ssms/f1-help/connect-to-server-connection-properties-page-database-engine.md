---
title: 서버에 연결(연결 속성 페이지) 데이터베이스 엔진 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttosqlserver.connectionproperties.f1
ms.assetid: edc1143c-6a47-4b02-92ab-441bdea8ea8a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 30382bcb0c70fb985c88866602cb997988b88569
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70153748"
---
# <a name="connect-to-server-connection-properties-page-database-engine"></a>서버에 연결(연결 속성 페이지) 데이터베이스 엔진
  인스턴스에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 연결 하거나 [!INCLUDE[ssDE](../../includes/ssde-md.md)] **등록 된 서버**에 등록할 때이 탭을 사용 하 여 옵션을 확인 하거나 지정할 수 있습니다. **연결** 및 **옵션** 은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결 하는 경우에만이 대화 상자에 나타납니다. **테스트** 및 **저장** 은 등록 [!INCLUDE[ssDE](../../includes/ssde-md.md)]시에만이 대화 상자에 나타납니다.  
  
## <a name="options"></a>옵션  
 **데이터베이스에 연결**  
 목록에서 연결할 데이터베이스를 선택합니다. ** \<기본>** 를 선택 하면 서버의 기본 데이터베이스에 연결 됩니다. ** \<서버>찾아보기 **를 선택 하는 경우 서버에서 연결할 데이터베이스를 찾아볼 수 있습니다.  
  
 를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 통해 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]데이터베이스 엔진 인스턴스에 연결할 때 인증을 사용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하 고 **서버에 연결** 대화 상자의 **연결 속성** 탭에서 데이터베이스를 지정 해야 합니다. **연결 암호화** 확인란을 선택 했는지 확인 합니다.  
  
 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 **master**에 연결됩니다. 사용자 데이터베이스를 지정하면 개체 탐색기에서 해당 데이터베이스와 해당 개체만 볼 수 있습니다. 
  **master**에 연결하면 모든 데이터베이스를 볼 수 있습니다. 자세한 내용은 [Azure SQL Database 개요](/azure/sql-database/sql-database-technical-overview)를 참조 하세요.  
  
 **네트워크 프로토콜**  
 목록에서 프로토콜을 선택합니다. 컴퓨터 관리에서 클라이언트 네트워크 구성을 사용하여 구성한 클라이언트 프로토콜을 사용할 수 있습니다.  
  
 **네트워크 패킷 크기**  
 전송할 네트워크 패킷의 크기를 입력합니다. 기본값은 4096바이트입니다.  
  
 **연결 시간 제한**  
 제한 시간이 초과 되기 전까지 연결이 설정 될 때까지 대기 하는 시간 (초)을 입력 합니다. 기본값은 15 초입니다.  
  
 **실행 제한 시간**  
 서버에서 태스크가 실행 완료되기까지 대기하는 시간(초)을 입력합니다. 기본값은 0초이며 시간 제한 없음을 의미합니다.  
  
 **연결 암호화**  
 연결 암호화를 강제 적용합니다.  
  
 **사용자 지정 색 사용**  
 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 창의 상태 표시줄 배경색을 지정하려는 경우 선택합니다. 색을 지정하려면 **선택**을 클릭합니다. 
  **색** 대화 상자의 **기본 색** 표에서 미리 정의된 색을 선택하거나 **사용자 지정 색 만들기** 를 클릭하여 사용자 지정 색을 정의하고 사용합니다.  
  
-   
  **개체 탐색기** 창에서 서버 항목에 대한 색을 지정하면 쿼리 편집기 창을 열 때 해당 색이 사용됩니다. 쿼리 편집기 창을 열려면 서버 항목을 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택하거나 **개체 탐색기** 창이 활성 상태이고 이 서버에 포커스가 있으면 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
-   
  **등록된 서버** 창에서 서버 항목에 대한 색을 지정하면 쿼리 편집기 창을 열 때 해당 색이 사용됩니다. 쿼리 편집기 창을 열려면 서버 항목을 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택하거나 **등록된 서버** 창이 활성 상태이고 이 서버에 포커스가 있으면 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
-   
  **파일** 메뉴에서 **새로 만들기** 를 클릭하고 **데이터베이스 엔진 쿼리**를 클릭하면 **서버에 연결** 대화 상자에서 지정한 색이 쿼리 편집기 창에 적용됩니다.  
  
 **모두 다시 설정**  
 수동으로 입력한 모든 연결 속성 값을 기본값으로 되돌립니다.  
  
 **연결**  
 목록에 있는 값을 사용하여 연결을 시도합니다.  
  
 **옵션**  
 대화 상자를 변경하여 암호 저장과 같은 추가 서버 연결 옵션을 숨기려면 클릭합니다.  
  
 **테스트할**  
 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 **등록된 서버**에 등록하는 경우 연결을 테스트하려면 클릭합니다.  
  
 **Save**  
 
  **등록된 서버**에 설정을 저장합니다.  
  
## <a name="see-also"></a>참고 항목  
 [연결 속성 대화 상자](../../database-engine/connection-properties-dialog-box.md)  
  
  
