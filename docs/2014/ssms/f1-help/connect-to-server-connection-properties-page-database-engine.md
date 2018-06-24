---
title: 서버에 연결(연결 속성 페이지) 데이터베이스 엔진 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.connecttosqlserver.connectionproperties.f1
ms.assetid: edc1143c-6a47-4b02-92ab-441bdea8ea8a
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f79ba89862334e19c3e50b347588de4e4183afaa
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080352"
---
# <a name="connect-to-server-connection-properties-page-database-engine"></a>서버에 연결(연결 속성 페이지) 데이터베이스 엔진
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스에 연결하거나 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 **등록된 서버**에 등록할 때 이 탭을 사용하여 옵션을 확인하거나 지정할 수 있습니다. **연결** 및 **옵션** 은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결 중인 경우에만 이 대화 상자에 나타납니다. **테스트** 및 **저장** 은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]등록 시에만 이 대화 상자에 나타납니다.  
  
## <a name="options"></a>변수  
 **데이터베이스에 연결**  
 목록에서 연결할 데이터베이스를 선택합니다. 선택 하는 경우  **\<기본 >**, 서버에 대 한 기본 데이터베이스에 연결 됩니다. 선택 하는 경우  **\<서버 찾아보기 >**, 데이터베이스를 연결 하는 데에 대 한 서버를 찾아볼 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 통해 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]데이터베이스 엔진 인스턴스에 연결할 때는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용해야 하며 **서버에 연결** 대화 상자의 **연결 속성** 탭에서 데이터베이스를 지정해야 합니다. **연결 암호화** 확인란을 선택해야 합니다.  
  
 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 **master**에 연결됩니다. 사용자 데이터베이스를 지정하면 개체 탐색기에서 해당 데이터베이스와 해당 개체만 볼 수 있습니다. **master**에 연결하면 모든 데이터베이스를 볼 수 있습니다. 자세한 내용은 [Microsoft Azure SQL Database 개요](http://go.microsoft.com/fwlink/?LinkId=163948)를 참조하세요.  
  
 **네트워크 프로토콜**  
 목록에서 프로토콜을 선택합니다. 컴퓨터 관리에서 클라이언트 네트워크 구성을 사용하여 구성한 클라이언트 프로토콜을 사용할 수 있습니다.  
  
 **네트워크 패킷 크기**  
 전송할 네트워크 패킷의 크기를 입력합니다. 기본값은 4096바이트입니다.  
  
 **연결 제한 시간**  
 제한 시간이 초과하기 전까지 연결을 대기하는 시간(초)을 입력합니다. 기본값은 15초입니다.  
  
 **실행 제한 시간**  
 서버에서 태스크가 실행 완료되기까지 대기하는 시간(초)을 입력합니다. 기본값은 0초이며 시간 제한 없음을 의미합니다.  
  
 **연결 암호화**  
 연결 암호화를 강제 적용합니다.  
  
 **사용자 지정 색 사용**  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 창의 상태 표시줄 배경색을 지정하려는 경우 선택합니다. 색을 지정하려면 **선택**을 클릭합니다. **색** 대화 상자의 **기본 색** 표에서 미리 정의된 색을 선택하거나 **사용자 지정 색 만들기** 를 클릭하여 사용자 지정 색을 정의하고 사용합니다.  
  
-   **개체 탐색기** 창에서 서버 항목에 대한 색을 지정하면 쿼리 편집기 창을 열 때 해당 색이 사용됩니다. 쿼리 편집기 창을 열려면 서버 항목을 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택하거나 **개체 탐색기** 창이 활성 상태이고 이 서버에 포커스가 있으면 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
-   **등록된 서버** 창에서 서버 항목에 대한 색을 지정하면 쿼리 편집기 창을 열 때 해당 색이 사용됩니다. 쿼리 편집기 창을 열려면 서버 항목을 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택하거나 **등록된 서버** 창이 활성 상태이고 이 서버에 포커스가 있으면 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
-   **파일** 메뉴에서 **새로 만들기** 를 클릭하고 **데이터베이스 엔진 쿼리**를 클릭하면 **서버에 연결** 대화 상자에서 지정한 색이 쿼리 편집기 창에 적용됩니다.  
  
 **모두 다시 설정**  
 수동으로 입력한 모든 연결 속성 값을 기본값으로 되돌립니다.  
  
 **연결**  
 목록에 있는 값을 사용하여 연결을 시도합니다.  
  
 **옵션**  
 대화 상자를 변경하여 암호 저장과 같은 추가 서버 연결 옵션을 숨기려면 클릭합니다.  
  
 **테스트**  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 **등록된 서버**에 등록하는 경우 연결을 테스트하려면 클릭합니다.  
  
 **저장**  
 **등록된 서버**에 설정을 저장합니다.  
  
## <a name="see-also"></a>관련 항목  
 [연결 속성 대화 상자](../../database-engine/connection-properties-dialog-box.md)  
  
  