---
title: Visual FoxPro 데이터 원본 추가 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 262e8487e8133cf1c312659fa2fc28276aafa07e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47706182"
---
# <a name="adding-a-visual-foxpro-data-source"></a>Visual FoxPro 데이터 원본 추가
응용 프로그램에서 Visual FoxPro 데이터에 액세스 하려면 데이터 원본을 사용 해야 합니다. 다음과 같이 데이터 소스를 만들 수 있습니다.  
  
-   Microsoft® Word, Microsoft Excel 또는 Microsoft Access 등의 응용 프로그램에서 ODBC 드라이버를 사용 하는 합니다.  
  
-   외부 응용 프로그램을 Microsoft Windows® 95, Microsoft Windows 98 또는 Microsoft Windows/Windows 2000 제어판을 사용합니다.  
  
 데이터 원본 시스템에 있으면 Visual FoxPro 데이터에 액세스 하려는 때마다 동일한 데이터 소스를 재사용할 수 있습니다. 여러 다른 데이터베이스 또는 테이블에 액세스 하려는 경우에 각 데이터베이스 또는 디렉터리에 대 한 별도 데이터 소스를 만들 수 있습니다.  
  
 다음 절차는 제어판을 사용 하 여 데이터 원본을 만듭니다. 응용 프로그램에서 데이터 원본을 만드는 방법에 대 한 자세한 내용은 참조 하세요. [Microsoft Office에서 Visual FoxPro 데이터 액세스](../../odbc/microsoft/accessing-visual-foxpro-data-from-microsoft-office.md)합니다.  
  
### <a name="to-add-a-visual-foxpro-data-source"></a>Visual FoxPro 데이터 원본을 추가 하려면  
  
1.  Windows 2000을 실행 하는 컴퓨터에서 Windows 제어판을 열고 관리 도구를 두 번 클릭 합니다.  
  
2.  데이터 원본 (ODBC) ODBC 데이터 원본 관리자 대화 상자를 열려면 두 번 클릭 합니다. Visual FoxPro ODBC 드라이버 또는 모든 ODBC 드라이버 소프트웨어를 설치한 후이 아이콘은 사용할 수 있습니다.  
  
    > [!NOTE]  
    >  이전 버전의 Windows 실행 하는 경우 Windows 제어판을 열고 32 비트 ODBC 또는 ODBC는 ODBC 데이터 원본 관리자 대화 상자를 열려면 두 번 클릭 합니다.  
  
3.  추가를 클릭합니다.  
  
4.  새 데이터 원본 만들기 대화 상자에서 Microsoft Visual FoxPro 드라이버를 선택 하 고 마침을 클릭 합니다.  
  
5.  에 [ODBC Visual FoxPro 설치 대화 상자가](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md), 데이터 원본 이름 및 설명을 입력, 데이터베이스 유형 선택, 데이터베이스 또는 디렉터리를 선택 및 확인을 클릭 합니다.  
  
     새 데이터 원본 이름은 ODBC 데이터 원본 관리자 대화 상자의 사용자 DSN 탭에서 사용자 데이터 원본 목록에 표시 됩니다.  
  
6.  새 데이터 원본을 저장 하 여 ODBC 데이터 원본 관리자 대화 상자를 닫으려면 확인을 클릭 합니다.
