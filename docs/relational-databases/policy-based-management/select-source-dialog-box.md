---
title: "원본 선택 대화 상자 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.dmf.selectsource.f1
ms.assetid: d664c2e5-dd0c-4da8-b27d-aa4ee4fc0ffd
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a8ffe2ca7e33b741309b594c0a351825fee59b07
ms.lasthandoff: 04/11/2017

---
# <a name="select-source-dialog-box"></a>원본 선택 대화 상자
  이 대화 상자를 사용하여 실행할 정책의 원본을 선택할 수 있습니다. 정책이 포함된 하나 이상의 XML 파일을 선택하려면 **파일**을 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 있는 정책을 실행하려면 **서버**를 선택합니다.  
  
 이 대화 상자는 여러 가지 방법으로 열 수 있습니다.  
  
 **이 대화 상자를 열려면**  
  
-   등록된 서버에서 **로컬 서버 그룹** , **로컬 서버 그룹**아래 서버 또는 **중앙 관리 서버**아래 서버를 마우스 오른쪽 단추로 클릭하고 **정책 평가**를 선택합니다. **정책 평가** 대화 상자에서 **정책 선택** 페이지에서 찾아보기 단추(**...**)를 클릭합니다.  
  
-   개체 탐색기에서 **관리**, **정책 관리**를 차례로 확장한 다음 **정책**을 마우스 오른쪽 단추로 클릭하고 **정책 가져오기**를 선택합니다. **가져오기** 대화 상자에서 찾아보기(**...**) 단추를 클릭합니다.  
  
-   개체 탐색기에서 서버, 데이터베이스 또는 데이터베이스 개체를 마우스 오른쪽 단추로 클릭하고 **정책**을 선택한 다음 **평가**를 선택합니다. **정책 평가** 대화 상자에서 **정책 선택** 페이지에서 찾아보기 단추(**...**)를 클릭합니다.  
  
## <a name="options"></a>옵션  
 **파일**  
 정책이 포함된 하나 이상의 XML 파일을 선택합니다.  
  
 **서버**  
 실행할 정책이 포함된 서버를 선택할 수 있도록 합니다.  
  
 **서버 유형**  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 서버만 정책을 포함합니다. 이 부분은 읽기 전용입니다.  
  
 **서버 이름**  
 연결할 서버 인스턴스를 선택합니다. 마지막으로 연결한 서버 인스턴스가 기본적으로 표시됩니다.  
  
 **인증**  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결할 때는 두 가지 인증 모드를 사용할 수 있습니다.  
  
 **Windows 인증 모드(Windows 인증)**  
 Windows 인증 모드에서는 사용자가 Windows 사용자 계정을 통해 연결할 수 있습니다.  
  
 **SQL Server 인증(SQL Server Authentication)**  
 사용자가 지정한 로그인 이름과 암호를 사용하여 트러스트되지 않은 연결로부터 연결하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 계정이 설정되고 지정한 암호가 전에 기록한 암호와 일치하는지를 확인하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 자체적으로 인증을 수행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 로그인 계정이 설정되어 있지 않으면 인증이 실패하고 오류 메시지가 나타납니다.  
  
> [!IMPORTANT]  
>  가능하면 Windows 인증을 사용하세요.  
  
 **사용자 이름**  
 연결에 사용할 사용자 이름을 입력합니다. 이 옵션은 Windows 인증을 사용하여 연결하도록 선택한 경우에만 사용할 수 있습니다.  
  
 **로그인**  
 연결 시 사용할 로그인을 입력합니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결하도록 선택한 경우에만 사용할 수 있습니다.  
  
 **암호**  
 로그인 암호를 입력합니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결하도록 선택한 경우에만 편집할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [정책 관리 노드&#40;개체 탐색기&#41;](../../relational-databases/policy-based-management/policy-management-node-object-explorer.md)   
 [정책 기반 관리를 사용하여 서버 관리](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
