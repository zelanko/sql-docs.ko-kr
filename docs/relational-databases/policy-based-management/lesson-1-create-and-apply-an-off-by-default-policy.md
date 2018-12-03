---
title: '1단원: Off By Default 정책 만들기 및 적용 | Microsoft 문서'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: security
ms.prod_service: database-engine
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: d31367db-b7db-44c4-8df2-f1240474cf78
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 678f9da12655cc733dcdf95aca5f61e5aa1cd45e
ms.sourcegitcommit: ca038f1ef180e4e1b27910bbc5d87822cd1ed176
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52158625"
---
# <a name="lesson-1-create-and-apply-an-off-by-default-policy"></a>1단원: Off By Default 정책 만들기 및 적용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
정책 기반 관리 정책을 사용하면 하나 이상의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스, 하나 이상의 인스턴스 개체, 서버 인스턴스, 하나 이상의 데이터베이스 또는 하나 이상의 데이터베이스 개체를 관리할 수 있습니다. 데이터베이스 관리자로서 특정 서버에 데이터베이스 메일이 설정되지 않도록 해야 하는 경우가 있습니다. 이 단원에서는 해당 서버 옵션을 설정하는 조건과 정책을 만듭니다. 서버가 정책을 준수하는지 여부를 확인하기 위해 해당 서버를 테스트합니다. 그런 다음 해당 정책을 통해 서버를 다시 구성하여 서버가 정책을 준수하도록 합니다.  

## <a name="prerequisites"></a>사전 요구 사항
이 자습서를 완료하려면 SQL Server Management Studio 및 SQL Server 인스턴스에 대한 액세스 권한이 필요합니다. 

- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)을 설치합니다.
  
## <a name="create-the-mail-off-condition"></a>mail-off 조건 만들기

1.  개체 탐색기에서 **관리**, **정책 관리**, **패싯**을 차례로 확장하고 **노출 영역 구성**을 마우스 오른쪽 단추로 클릭한 다음 **새 조건**을 클릭합니다.  

    ![새 조건](Media/lesson-1-create-and-apply-an-off-by-default-policy/new-surface-area-condition.png)
  
2.  **새 조건 만들기** 대화 상자의 **이름** 상자에 **Mail Off**를 입력합니다.   
    1. **패싯** 상자에서 **노출 영역 구성** 패싯이 선택되어 있는지 확인합니다.
    1. **식** 영역의 **필드** 상자에서 **@DatabaseMailEnabled**를 선택하고, **연산자** 상자에서 **=** 를 선택한 다음 **값**에서 **False**를 선택합니다.  
    1. **설명** 페이지에서 조건에 대한 설명을 입력한 다음 **확인** 을 클릭하여 조건을 만듭니다.  

    ![Mail off 조건](Media/lesson-1-create-and-apply-an-off-by-default-policy/mail-off-condition.png) 
  
## <a name="create-the-off-by-default-policy"></a>off-by-default 정책 만들기  
  
1.  개체 탐색기에서 **노출 영역 구성**을 마우스 오른쪽 단추로 클릭한 다음 **새 정책**을 클릭합니다.  
  
2.  **새 정책 만들기** 대화 상자의 **이름** 상자에 **Off By Default**를 입력합니다. 
    1. **사용** 확인란을 선택하지 않은 상태로 둡니다. **사용** 확인란은 자동화된 정책에 적용되며 이 정책은 요청 시 실행됩니다.
    1. **조건 확인** 확인란에서 **노출 영역 구성** 영역까지 아래로 스크롤한 다음 **Mail Off** 를 확인할 조건으로 선택합니다.
    1. 이 정책은 서버 범위 정책이므로 **적용 대상** 상자는 비어 있습니다. 
    1. **평가 모드** 확인란에서 **요청 시** 를 평가 모드로 선택합니다.
    1. **서버 제한** 확인란에서 **없음**을 선택합니다.
    1. **설명** 페이지에서 정책에 대한 설명을 입력합니다.  

    ![off by default 정책](Media/lesson-1-create-and-apply-an-off-by-default-policy/off-by-default-policy.png)
  
9. 설명 페이지에서 **추가 도움말 하이퍼링크** 영역에 정책에 대한 웹 페이지의 하이퍼링크를 제공할 수 있습니다. **표시할 텍스트** 상자에 하이퍼링크에 대해 표시할 텍스트를 입력합니다.
    1. **주소** 상자에 회사의 IT 부서에 대한 홈페이지와 같이 도움말 페이지에 대한 하이퍼링크를 입력합니다.
    1. 웹 페이지를 열어 주소를 확인하려면 **링크 테스트**를 클릭합니다.
    1. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

    ![Off-by-default 정책 웹 링크](Media/lesson-1-create-and-apply-an-off-by-default-policy/off-by-default-policy-web-link.png)


## <a name="configure-server-to-run-off-by-default-policy"></a>off-by-default 정책을 실행하도록 서버 구성 

1.  개체 탐색기에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 마우스 오른쪽 단추로 클릭하고 **정책**을 가리킨 다음 **평가**를 클릭합니다.  

    ![정책 평가](Media/lesson-1-create-and-apply-an-off-by-default-policy/evaluate-policy.png)
  
2.  **정책 평가** 대화 상자에서는 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 또는 파일에서 정책을 선택할 수 있습니다. 이 단계를 위해서 **원본** 을 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스로 설정해 둡니다.  
    1. **정책** 섹션에서 **Off By Default** 정책을 선택합니다.
    1. 서버가 정책을 준수하는지 여부를 확인하려면 **평가**를 클릭합니다.
    1. **이 정책을 준수하는 경우** 결과 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 영역에 확인 표시가 있는 녹색 원이 나타납니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 정책을 준수하지 않는 경우 X 표시가 있는 빨간색 원이 나타납니다. 

   ![off-by-default 정책 평가](Media/lesson-1-create-and-apply-an-off-by-default-policy/evaluate-off-by-default-policy.png)

  
6.  오류가 발생할 경우 **대상 정보** 영역의 **메시지** 열에서 추가 정보를 볼 수 있습니다. **메시지** 열에서 **보기** 를 클릭하여 검사한 각 패싯 속성에 대한 검사 결과를 포함하는 보고서를 볼 수 있습니다. 

    ![정책 평가 결과 보기 ](Media/lesson-1-create-and-apply-an-off-by-default-policy/view-results-of-policy-evaluation.png)
  
7.  정책 설명이 페이지 아래쪽에 표시되고 **추가 도움말** 섹션에서 정책에 대해 구성한 하이퍼링크를 표시합니다. 메시지 하이퍼링크를 클릭하여 정책을 만들 때 지정한 웹 페이지를 엽니다.   

1.  브라우저를 닫은 다음 **결과 자세히 보기** 대화 상자를 닫습니다.  

1. 서버가 정책을 준수하지 않고, 데이터베이스 메일을 사용하지 않으려는 경우 **평가 결과** 페이지에서 **적용** 을 클릭합니다.  
  
10. **결과 자세히 보기** 대화 상자와 **정책 평가** 대화 상자를 모두 닫습니다.   

   
## <a name="next-lesson"></a>다음 단원  
[2단원: 명명 표준 정책 만들기 및 적용](../../relational-databases/policy-based-management/lesson-2-create-and-apply-a-naming-standards-policy.md)  
  
  
  
