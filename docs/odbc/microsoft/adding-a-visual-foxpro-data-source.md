---
title: 비주얼 폭스프로 데이터 소스 추가 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro data source [ODBC], adding
- adding data sources [ODBC], Visual FoxPro ODBC driver
ms.assetid: 1487e188-52c8-4f48-b4fe-25a650dd9e97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1fd0c0f929ca00b7cf731dc92f07f69b6503f884
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307144"
---
# <a name="adding-a-visual-foxpro-data-source"></a>Visual FoxPro 데이터 원본 추가
응용 프로그램에서 Visual FoxPro 데이터에 액세스하려면 데이터 원본이 있어야 합니다. 다음과 같이 데이터 원본을 만들 수 있습니다.  
  
-   ODBC 드라이버를 사용하는 마이크로 소프트® 워드, 마이크로 소프트 엑셀 또는 마이크로 소프트 액세스와 같은 응용 프로그램에서.  
  
-   응용 프로그램 외부, 마이크로 소프트 윈도우를 사용하여® 95, 마이크로 소프트 윈도우 98, 또는 마이크로 소프트 윈도우 NT® / 윈도우 2000 제어판.  
  
 시스템에 데이터 원본이 있으면 Visual FoxPro 데이터에 액세스하려는 때마다 동일한 데이터 원본을 다시 사용할 수 있습니다. 액세스하려는 여러 데이터베이스 또는 테이블이 있는 경우 각 데이터베이스 또는 디렉터리에 대해 별도의 데이터 원본을 만들 수 있습니다.  
  
 다음 절차에서 제어판을 사용하여 데이터 원본을 만듭니다. 응용 프로그램에서 데이터 원본을 만드는 방법에 대한 자세한 내용은 [Microsoft Office의 Visual FoxPro 데이터 액세스를](../../odbc/microsoft/accessing-visual-foxpro-data-from-microsoft-office.md)참조하십시오.  
  
### <a name="to-add-a-visual-foxpro-data-source"></a>비주얼 FoxPro 데이터 원본을 추가하려면  
  
1.  Windows 2000을 실행하는 컴퓨터에서는 Windows 제어판을 열고 관리 도구를 두 번 클릭합니다.  
  
2.  ODBC(데이터 원본)를 두 번 클릭하여 ODBC 데이터 원본 관리자 대화 상자를 엽니다. 이 아이콘은 Visual FoxPro ODBC 드라이버 또는 ODBC 드라이버 소프트웨어를 설치한 후에 사용할 수 있습니다.  
  
    > [!NOTE]  
    >  이전 버전의 Windows를 실행 중인 경우 Windows 제어판을 열고 32비트 ODBC 또는 ODBC를 두 번 클릭하여 ODBC 데이터 원본 관리자 대화 상자를 엽니다.  
  
3.  추가를 클릭합니다.  
  
4.  새 데이터 원본 만들기 대화 상자에서 Microsoft Visual FoxPro 드라이버를 선택한 다음 완료를 클릭합니다.  
  
5.  [ODBC Visual FoxPro 설치 대화 상자에서](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)데이터 원본 이름과 설명을 입력하고 데이터베이스 유형을 선택하고 데이터베이스 또는 디렉터리를 선택한 다음 확인을 클릭합니다.  
  
     새 데이터 원본 이름은 ODBC 데이터 원본 관리자 대화 상자의 사용자 DSN 탭에 있는 사용자 데이터 원본 목록에 표시됩니다.  
  
6.  확인을 클릭하여 새 데이터 원본을 저장하고 ODBC 데이터 원본 관리자 대화 상자를 닫습니다.
