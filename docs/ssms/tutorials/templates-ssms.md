---
Title: 'Tutorial: Using templates in SQL Server Management Studio'
description: SSMS에서 템플릿 사용에 대한 자습서입니다.
keywords: SQL Server, SSMS, SQL Server Management Studio, 템플릿
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod: sql
ms.technology: ssms
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
ms.openlocfilehash: 539906b1a09838e43e34be96e4ee32daec19fab7
ms.sourcegitcommit: b5ab9f3a55800b0ccd7e16997f4cd6184b4995f9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34455227"
---
# <a name="tutorial-using-templates-in-sql-server-management-studio"></a>자습서: SQL Server Management Studio에서 템플릿 사용
이 자습서에서는 SSMS(SQL Server Management Studio)에서 사용할 수 있는 미리 빌드된 T-SQL(Transact-SQL) 템플릿을 소개합니다. 이 아티클에서는 다음과 같은 방법을 알아봅니다.

> [!div class="checklist"]
> * 템플릿 탐색기를 사용하여 T-SQL 스크립트 생성
> * 기존 템플릿 편집 
> * 디스크에서 템플릿 찾기
> * 새 템플릿 만들기
   

## <a name="prerequisites"></a>사전 요구 사항
이 자습서를 완료하려면 SQL Server Management Studio 및 SQL Server에 대한 액세스 권한이 필요합니다. 

- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)을 설치합니다.

 

## <a name="use-template-browser"></a>템플릿 탐색기 사용
이 섹션에서는 템플릿 탐색기를 찾고 사용하는 방법을 알아봅니다. 

1. SQL Server Management Studio를 엽니다.
2. **보기** 메뉴에서 **템플릿 탐색기**(Ctrl + Alt + T)를 선택합니다. 

    ![템플릿 탐색기 열기](media/templates-ssms/templatebrowser.png)
    
    템플릿 탐색기의 맨 아래에서 최근에 사용한 템플릿을 확인할 수 있습니다.

3. 관심 있는 노드를 확장합니다. 템플릿을 마우스 오른쪽 단추로 클릭한 다음, **열기**를 선택합니다.

    ![템플릿 열기](media/templates-ssms/opentemplate.png)
    
    열려는 템플릿 이름을 두 번 클릭하면 됩니다.

4. 새 쿼리 창이 열립니다. T-SQL 스크립트가 이미 채워집니다. 
5. 필요에 맞게 템플릿을 수정한 다음, **실행**을 선택하여 쿼리를 실행합니다.
    
    ![DB 템플릿 만들기](media/templates-ssms/createdbtemplate.png)


## <a name="edit-an-existing-template"></a>기존 템플릿 편집
템플릿 탐색기에서 기존 템플릿을 편집할 수도 있습니다.  

1. 템플릿 브라우저에서 작업하려는 템플릿으로 이동합니다.
2. 템플릿을 마우스 오른쪽 단추로 클릭한 다음, **편집**을 선택합니다.

    ![템플릿 편집](media/templates-ssms/edittemplate.png)

3. 쿼리 창이 열리면 원하는 대로 변경합니다.
4. 템플릿을 저장하려면 **파일** > **저장**(Ctrl + S)을 선택합니다.
5. 쿼리 창을 닫습니다.
6. 템플릿을 다시 엽니다. 편집 내용이 표시되어야 합니다.
 

## <a name="locate-templates-on-disk"></a>디스크에서 템플릿 찾기
템플릿이 열리면 디스크에 있는 템플릿을 찾을 수 있습니다.

1. 템플릿 탐색기에서 템플릿을 선택한 다음, **편집**을 선택합니다.
2. **쿼리 제목**을 마우스 오른쪽 단추로 클릭한 다음, **상위 폴더 열기**를 선택합니다. 탐색기는 템플릿을 디스크에 저장한 위치를 열어야 합니다. 

   ![디스크의 템플릿](media/templates-ssms/templatesondisk.png)
  

## <a name="create-a-new-template"></a>새 템플릿 만들기
템플릿 브라우저에서 새 템플릿을 만들 수도 있습니다. 다음 단계에서는 새 폴더를 만든 다음, 해당 폴더에서 새 템플릿을 만드는 방법을 보여줍니다. 다음 단계를 사용하여 기존 폴더에 사용자 지정 템플릿을 만들 수도 있습니다. 

1. 템플릿 탐색기를 엽니다.
2. **SQL Server 템플릿**을 마우스 오른쪽 단추로 클릭한 다음, **새로 만들기** > **폴더**를 선택합니다.
3. 이 폴더의 이름을 **사용자 지정 템플릿**으로 지정합니다.

    ![사용자 지정 템플릿 폴더 만들기](media/templates-ssms/creatingcustomtemplate.png)

4. 새로 만든 사용자 지정 템플릿 폴더를 마우스 오른쪽 단추로 클릭한 다음, **새로 만들기** > **템플릿**을 선택합니다. 템플릿의 이름을 입력합니다.
 
    ![사용자 지정 템플릿 만들기](media/templates-ssms/createnewtemplate.png)
   
5. 만든 템플릿을 마우스 오른쪽 단추로 클릭한 다음, **편집**을 선택합니다. 새 쿼리 창이 열립니다.
6. 저장하려는 T-SQL 텍스트를 입력합니다. 
7. **파일** 메뉴에서 **저장**을 선택합니다.
8. 기존 쿼리 창을 닫은 다음, 새 사용자 지정 템플릿을 엽니다. 

    

## <a name="next-steps"></a>다음 단계
다음 아티클에서는 SQL Server Management Studio를 사용하기 위한 추가 팁과 요령을 제공합니다. 

> [!div class="nextstepaction"]
> [SSMS 사용을 위한 추가 팁과 요령](ssms-tricks.md)
