---
title: '작업 2: Excel용 MDS 추가 기능을 사용 하 여 MDS에 공급자 데이터 업로드 Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 598deb57-e0cc-4e0a-aeb1-94432c094c67
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 5e825829eb70b695a619df8caaa59788d0ad413f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064768"
---
# <a name="task-2-uploading-supplier-data-to-mds-using-mds-add-in-for-excel"></a>태스크 2: Excel용 MDS 추가 기능을 사용하여 MDS에 공급자 데이터 업로드
  이 작업에서는 **Excel용 MDS 추가 기능**를 사용 하 여 정리 된 데이터와 공급자 데이터를 **MDS** 에 게시 합니다. 이전 단원에서 만든 **Suppliers** 모델에 **공급자** 라는 엔터티를 만듭니다. 이 엔터티는 Excel 파일의 각 열에 대한 특성을 갖습니다. 공급자 엔터티의 Code 및 Name 특성은 Excel의 공급자 이름 및 **공급자** **이름** 열에 해당 합니다.  
  
1.  **Excel**에서 **정리 및 일치 Suppliers.xls** 을 엽니다.  
  
2.  **Ctrl + A** 를 눌러 전체 데이터를 선택 합니다. 스프레드시트에서 전체 데이터를 선택 하는 것이 **중요** 합니다.  
  
3.  메뉴 모음에서 **마스터 데이터** 를 클릭합니다.  
  
4.  리본에서 **엔터티 만들기** 단추를 클릭 합니다.  
  
     ![Excel - 마스터 데이터 탭 - 엔터티 만들기 단추](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-01.jpg "Excel - 마스터 데이터 탭 - 엔터티 만들기 단추")  
  
5.  **연결 관리** 대화 상자에서 **기존 연결** 아래에 **로컬 MDS 서버**에 대한 연결이 표시되지 않으면 다음을 수행합니다.  
  
    1.  **새 연결 만들기**를 선택하고 **새로 만들기** 단추를 클릭합니다.  
  
    2.  **새 연결 추가** 대화 상자에서 **설명** 에 **Local MDS server** 를 입력 하 고/localhost/MDS **서버 주소**에는 **http: \/ ** 를 입력 한 다음 **확인** 을 클릭 하 여 대화 상자를 닫습니다.  
  
6.  **연결 관리** 대화 상자에서 **로컬 MDS 서버** ()를 선택 하 고 `http://localhost/MDS` **테스트** 를 클릭 하 여 연결을 테스트 합니다. 메시지 상자에서 **확인** 을 클릭합니다.  
  
7.  **연결** 을 클릭 하 여 MDS 서버에 연결 합니다.  
  
8.  **엔터티 만들기** 대화 상자에서 **모델**에 대해 **Suppliers** 를 선택 합니다.  
  
9. **버전**에 대해 **VERSION_1** 가 선택 되어 있는지 확인 합니다.  
  
10. **새 엔터티 이름**에 대해 **공급자** 를 입력 합니다.  
  
11. **고유 식별자 필드를 포함 하는 열** 에 대해 **공급자** 를 선택 합니다 (코드를 자동으로 생성할 수도 있음). 기본적으로 **Excel** 의 공급자 **열을** **공급자** 엔터티의 **Code** 특성에 매핑합니다.  
  
12. 이름 필드를 **포함 하는 열** 에 대해 **공급자 이름** 을 선택 합니다. 기본적으로 **Excel** 의 **공급자 이름** 열을 **공급자** 엔터티의 **name** 특성에 매핑합니다. **코드** 및 **이름** 특성은 MDS의 엔터티에 대 한 필수 특성입니다.  
  
     ![엔터티 만들기 대화 상자](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-02.jpg "엔터티 만들기 대화 상자")  
  
13. **확인** 을 클릭 하 여 MDS에서 엔터티를 만들고, 엔터티에 마스터 데이터를 게시 하 고, **엔터티 만들기** 대화 상자를 닫습니다.  
  
14. 이제 엔터티의 이름인 **공급자**라는 새 시트가 표시 됩니다 .이 시트에는 Excel 스프레드시트에 추가 되 고 워크시트의 맨 위에는 해당 워크시트가 MDS 서버에 연결 되어 있음을 확인 해야 합니다. 원본 워크시트 ( **Sheet1**제목)는 여전히 존재 합니다.  
  
     ![Excel - 공급자 및 Sheet1 탭](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-03.jpg "Excel - 공급자 및 Sheet1 탭")  
  
     ![Excel - MDS 연결 정보 표시](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-04.jpg "Excel - MDS 연결 정보 표시")  
  
15. **Excel** 을 열어 둡니다.  
  
## <a name="next-task"></a>다음 태스크  
 [태스크 3: 마스터 데이터 관리자에서 데이터 확인](../../2014/tutorials/task-3-verifying-the-data-in-master-data-manager.md)  
  
  
