---
Title: 'Tutorial: Using Templates in SQL Server Management Studio'
description: SSMS 내에서 템플릿 사용에 대한 자습서입니다. 의 인스턴스에 액세스할 때마다 SQL Server 로그인을 제공할 필요가 없습니다.
keywords: SQL Server, SSMS, SQL Server Management Studio, 템플릿
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
helpviewer_keywords:
- templates [SQL Server], SQL Server Management Studio
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- SQL Server Management Studio [SQL Server], tutorials
- scripts [SQL Server], SQL Server Management Studio
ms.openlocfilehash: 05a9883ff436991e5ee830ce1561ecced0fa9b60
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/21/2018
---
# <a name="tutorial-using-templates-within-sql-server-management-studio"></a>자습서: SQL Server Management Studio 내에서 템플릿 사용
이 자습서에서는 SSMS(SQL Server Management Studio) 내에서 사용할 수 있는 미리 빌드된 T-SQL(Transact-SQL) 템플릿을 소개합니다. 이 문서에서는 다음 작업 방법을 배웁니다.
    - 템플릿 탐색기를 사용하여 T-SQL 스크립트 생성
    - 기존 템플릿 편집 
    - 디스크에서 템플릿 찾기
    - 새 템플릿 만들기
   

## <a name="prerequisites"></a>사전 요구 사항
이 자습서를 완료하려면 SQL Server Management Studio 및 SQL Server에 대한 액세스가 필요합니다. 

- [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)을 설치합니다.

 

## <a name="using-the-template-browser"></a>템플릿 탐색기 사용
이 섹션에서는 **템플릿 탐색기**를 찾고 사용하는 방법을 알아봅니다. 

1. SQL Server Management Studio를 시작합니다.
2. **보기** 메뉴 > **템플릿 탐색기**(Ctrl + Alt + T)에서: 

    ![템플릿 탐색기](media/templates-ssms/templatebrowser.png)
    - **템플릿 탐색기**의 맨 아래에서 최근에 사용한 템플릿을 확인할 수도 있습니다.

3. 원하는 노드를 확장하고 마우스 오른쪽 단추로 템플릿 > 열기를 클릭합니다.

    ![템플릿 열기](media/templates-ssms/opentemplate.png)
    - 템플릿을 두 번 클릭하면 동일한 효과를 얻습니다.

4. T-SQL이 이미 채워진 새 쿼리 창을 시작합니다. 
5. 필요에 맞게 템플릿을 수정한 다음, 쿼리를 **실행합니다**.
    
    ![DB 템플릿 만들기](media/templates-ssms/createdbtemplate.png)


## <a name="edit-an-existing-template"></a>기존 템플릿 편집
**템플릿 탐색기** 내에서 기존 템플릿을 편집할 수도 있습니다.  

1. **템플릿 탐색기**에서 원하는 템플릿을 찾습니다.
2. 마우스 오른쪽 단추로 템플릿 > **편집**을 클릭합니다.

    ![템플릿 편집](media/templates-ssms/edittemplate.png)

3. 열려 있는 쿼리 창에서 원하는 대로 변경합니다.
4. **파일** > **저장**(Ctrl + S)으로 이동하여 템플릿을 저장합니다.
5. 쿼리 창을 닫습니다.
6. 새 편집이 있어야 하는 저장한 템플릿을 다시 엽니다.
 

## <a name="locate-the-templates-on-disk"></a>디스크에서 템플릿 찾기
템플릿이 열리면 디스크에서 찾을 수 있습니다.

1. **템플릿 탐색기** > **편집**에서 템플릿을 선택합니다.
2. 마우스 오른쪽 단추로 **쿼리 제목** > **상위 폴더 열기**를 클릭합니다. 템플릿이 디스크에서 저장되는 탐색기를 열어야 합니다. 

    ![디스크의 템플릿](media/templates-ssms/templatesondisk.png)
  

## <a name="create-a-new-template"></a>새 템플릿 만들기
**템플릿 탐색기** 내에서 새 템플릿을 만들 수도 있습니다. 이러한 단계는 새 폴더를 만든 다음, 해당 폴더 내에 새 템플릿을 만드는 방법을 설명합니다. 그러나 이 단계를 사용하여 기존 폴더 내에서 사용자 지정 템플릿을 만들 수도 있습니다. 

1. **템플릿 탐색기**를 엽니다.
2. 마우스 오른쪽 단추로 SQL Server 템플릿 > **새로 만들기** > **폴더**를 클릭합니다. 
3. 이 폴더의 이름을 **사용자 지정 템플릿**으로 지정합니다.

    ![사용자 지정 템플릿 만들기](media/templates-ssms/creatingcustomtemplate.png)

4. 마우스 오른쪽 단추로 새로 만든 **사용자 지정 템플릿** 폴더 > **새로 만들기** > **템플릿** > 템플릿 이름 지정을 클릭합니다. 
 
    ![사용자 지정 템플릿 만들기](media/templates-ssms/createnewtemplate.png)
   
5. 마우스 오른쪽 단추로 방금 만든 템플릿 > **편집**을 클릭합니다. **새 쿼리 창**을 엽니다.
6. 저장하려는 T-SQL 텍스트에 입력합니다. 
7. **파일** 메뉴 > **저장**으로 이동하여 파일을 저장합니다.
8. 기존 **쿼리 창**을 닫고 새 사용자 지정 템플릿을 엽니다. 

    

## <a name="next-steps"></a>다음 단계
다음 문서에서는 SQL Server Management Studio를 사용하기 위한 몇 가지 추가 팁과 요령을 제공합니다. 

자세히 알아보려면 다음 문서로 진행합니다.
> [!div class="nextstepaction"]
> [다음 단계 단추](ssms-tricks.md))
