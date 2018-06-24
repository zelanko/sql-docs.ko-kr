---
title: '작업 2: Excel 용 MDS 추가 기능을 사용 하 여 MDS에 공급자 데이터를 업로드 하 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 598deb57-e0cc-4e0a-aeb1-94432c094c67
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 1831fc9ea79027e24d752d05e3b50d3a58d6e06f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081011"
---
# <a name="task-2-uploading-supplier-data-to-mds-using-mds-add-in-for-excel"></a>태스크 2: Excel용 MDS 추가 기능을 사용하여 MDS에 공급자 데이터 업로드
  이 작업에서는 정리 및 공급 업체 데이터를 게시할 **MDS** 를 사용 하는 **MDS 추가 기능 Excel 용**합니다. 라는 엔터티를 만들고 **공급 업체** 에 **Suppliers** 이전 단원에서 만든 모델입니다. 이 엔터티는 Excel 파일의 각 열에 대한 특성을 갖습니다. Supplier 엔터티의 Code 및 Name 특성에 해당 하는 **SupplierID** 및 **Supplier Name** Excel의 열입니다.  
  
1.  열기 **정리 및 일치 Suppliers.xls** 에 **Excel**합니다.  
  
2.  키를 눌러 **CTRL + A** 전체 데이터를 선택 합니다. **중요** 스프레드시트에서 전체 데이터를 선택 합니다.  
  
3.  메뉴 모음에서 **마스터 데이터** 를 클릭합니다.  
  
4.  클릭 **엔터티 만들기** 리본의 단추입니다.  
  
     ![Excel-마스터 데이터 탭-엔터티 만들기 단추](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-01.jpg "Excel-마스터 데이터 탭-엔터티 만들기 단추")  
  
5.  **연결 관리** 대화 상자에서 **기존 연결** 아래에 **로컬 MDS 서버**에 대한 연결이 표시되지 않으면 다음을 수행합니다.  
  
    1.  **새 연결 만들기**를 선택하고 **새로 만들기** 단추를 클릭합니다.  
  
    2.  에 **새 연결 추가** 대화 상자에서 **로컬 MDS 서버** 에 대 한 **설명** 및 **http://localhost/MDS** 에 대 한  **MDS 서버 주소**를 클릭 하 고 **확인** 대화 상자를 닫습니다.  
  
6.  **연결 관리** 대화 상자에서 **로컬 MDS 서버** (http://localhost/MDS), 클릭 **테스트** 연결을 테스트 합니다. 메시지 상자에서 **확인** 을 클릭합니다.  
  
7.  클릭 **연결** MDS 서버에 연결 합니다.  
  
8.  에 **엔터티 만들기** 대화 상자에서 **Suppliers** 에 대 한는 **모델**합니다.  
  
9. 되도록 **VERSION_1** 에 대해 선택 된 **버전**합니다.  
  
10. 입력 **공급 업체** 에 대 한 **새 엔터티 이름**합니다.  
  
11. 선택 **SupplierID** 에 대 한 **고유 식별자를 포함 하는 열** 필드 (생성할 수도 있습니다 코드를 자동으로). 기본적으로 매핑하는 **SupplierID** 열에 **Excel** 에 **코드** 특성 **공급 업체** 엔터티.  
  
12. 선택 **Supplier Name** 에 대 한 **이름이 포함 된 열** 필드입니다. 기본적으로 매핑하는 **Supplier Name** 열에 **Excel** 에 **이름** 특성에는 **공급 업체** 엔터티. **코드** 및 **이름** 특성은 MDS에서 엔터티의 필수 특성입니다.  
  
     ![엔터티 만들기 대화 상자](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-02.jpg "엔터티 만들기 대화 상자")  
  
13. 클릭 **확인** MDS에서 엔터티를 만들려면를 엔터티에 마스터 데이터를 게시 하 고 닫습니다 **엔터티 만들기** 대화 상자.  
  
14. 이제 제목의 새 시트가 나타납니다 **공급 업체**, Excel 스프레드시트에 추가 된 엔터티의 이름인 및 워크시트의 맨 위쪽에 표시 되어야 워크시트가 MDS 서버에 연결 되어 있습니다. 원래 워크시트 (이라는 **Sheet1**) 여전히 존재 합니다.  
  
     ![Excel-공급자 및 Sheet1 탭](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-03.jpg "Excel-공급자 및 Sheet1 탭")  
  
     ![Excel-MDS 연결 정보를 보여 주는](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-04.jpg "Excel-MDS 연결 정보 표시")  
  
15. 유지 **Excel** 엽니다.  
  
## <a name="next-task"></a>다음 태스크  
 [태스크 3: 마스터 데이터 관리자에서 데이터 확인](../../2014/tutorials/task-3-verifying-the-data-in-master-data-manager.md)  
  
  