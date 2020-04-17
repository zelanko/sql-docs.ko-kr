---
title: '작업 2: 엑셀용 MDS 애드인을 사용하여 공급업체 데이터를 MDS에 업로드 | 마이크로 소프트 문서'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 598deb57-e0cc-4e0a-aeb1-94432c094c67
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 4e3cd4cecd88bcad83c6e9f2a59ecd5f225fb02a
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487697"
---
# <a name="task-2-uploading-supplier-data-to-mds-using-mds-add-in-for-excel"></a>태스크 2: Excel용 MDS 추가 기능을 사용하여 MDS에 공급자 데이터 업로드
  이 작업에서는 **Excel에 대한 MDS 추가 기능을**사용하여 정리된 및 공급자 데이터를 **MDS에** 게시합니다. 이전 단원에서 만든 **공급자** 모델에서 **공급자라는** 엔터티를 만듭니다. 이 엔터티는 Excel 파일의 각 열에 대한 특성을 갖습니다. 공급자 엔터티의 코드 및 이름 특성은 Excel의 **SupplierID** 및 **공급자 이름** 열에 해당합니다.  
  
1.  **Excel에서** **클렌징 및 일치 공급 업체.xls를 엽니다.**  
  
2.  **CTRL+A를** 눌러 전체 데이터를 선택합니다. 스프레드시트에서 전체 데이터를 선택하는 **것이 중요합니다.**  
  
3.  메뉴 모음에서 **마스터 데이터** 를 클릭합니다.  
  
4.  리본에서 **엔터티 만들기** 단추를 클릭합니다.  
  
     ![Excel - 마스터 데이터 탭 - 엔터티 만들기 단추](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-01.jpg "Excel - 마스터 데이터 탭 - 엔터티 만들기 단추")  
  
5.  **연결 관리** 대화 상자에서 **기존 연결** 아래에 **로컬 MDS 서버**에 대한 연결이 표시되지 않으면 다음을 수행합니다.  
  
    1.  **새 연결 만들기**를 선택하고 **새로 만들기** 단추를 클릭합니다.  
  
    2.  새 **연결 추가** 대화 상자에서 **Local MDS Server** **설명** 및 **http:\/MDS 서버 주소에 대한 /localhost/MDS를** 입력하고 **확인을** 클릭하여 대화 상자를 닫습니다. **MDS server address**  
  
6.  **연결 관리** 대화 상자에서 **로컬 MDS 서버** ()`http://localhost/MDS`)를 선택하여 **테스트를** 클릭하여 연결을 테스트합니다. 메시지 상자에서 **확인** 을 클릭합니다.  
  
7.  **MDS** 서버에 연결하려면 연결을 클릭합니다.  
  
8.  엔터티 **만들기** 대화 상자에서 **모델에**대한 **공급자를** 선택합니다.  
  
9. 버전 에 대해 **VERSION_1** 선택되어 있는지 **확인합니다.**  
  
10. **새 엔터티 이름에**대 한 **공급자를** 입력합니다.  
  
11. **고유 식별자 필드가 포함된 열에** 대해 **SupplierID를** 선택합니다(코드를 자동으로 생성할 수도 있음). 기본적으로 **Excel의** **SupplierID** 열을 **공급자** 엔터티의 **코드** 특성에 매핑합니다.  
  
12. **이름 필드가 포함된 열에** 대한 **공급자 이름을** 선택합니다. 기본적으로 **Excel의** **공급자 이름** 열을 **공급자** 엔터티의 **Name** 특성에 매핑합니다. **코드** 및 **이름** 특성은 MDS의 엔터티에 대한 필수 특성입니다.  
  
     ![엔터티 만들기 대화 상자](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-02.jpg "엔터티 만들기 대화 상자")  
  
13. **확인을** 클릭하여 MDS에서 엔터티를 만들고, 마스터 데이터를 엔터티에 게시하고, 엔터티 만들기 대화 **상자를** 닫습니다.  
  
14. 이제 엔터티 이름인 **Supplier라는**새 시트가 Excel 스프레드시트에 추가되고 워크시트 맨 위에 워크시트가 MDS 서버에 연결되어 있는지 확인할 수 있습니다. 원래 **워크시트(시트1)는**여전히 존재합니다.  
  
     ![Excel - 공급자 및 Sheet1 탭](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-03.jpg "Excel - 공급자 및 Sheet1 탭")  
  
     ![Excel - MDS 연결 정보 표시](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-04.jpg "Excel - MDS 연결 정보 표시")  
  
15. **Excel을** 열어 두십시오.  
  
## <a name="next-task"></a>다음 태스크  
 [태스크 3: 마스터 데이터 관리자에서 데이터 확인](../../2014/tutorials/task-3-verifying-the-data-in-master-data-manager.md)  
  
  
