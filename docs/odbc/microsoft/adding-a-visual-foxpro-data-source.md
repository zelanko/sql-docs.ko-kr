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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1fd0c0f929ca00b7cf731dc92f07f69b6503f884
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307144"
---
# <a name="adding-a-visual-foxpro-data-source"></a>Visual FoxPro 데이터 원본 추가
응용 프로그램에서 Visual FoxPro 데이터에 액세스 하려면 데이터 원본이 있어야 합니다. 다음과 같이 데이터 소스를 만들 수 있습니다.  
  
-   Microsoft® Word, microsoft Excel 또는 Microsoft Access와 같은 응용 프로그램에서 ODBC 드라이버를 사용 합니다.  
  
-   응용 프로그램 외부에서 Microsoft Windows® 95, Microsoft Windows 98 또는 Microsoft Windows NT®/Windows 2000 제어판을 사용 합니다.  
  
 시스템에 데이터 원본이 있으면 Visual FoxPro 데이터에 액세스할 때마다 동일한 데이터 원본을 다시 사용할 수 있습니다. 액세스 하려는 데이터베이스가 여러 개 있는 경우 각 데이터베이스 또는 디렉터리에 대 한 별도의 데이터 원본을 만들 수 있습니다.  
  
 다음 절차는 제어판을 사용 하 여 데이터 소스를 만듭니다. 응용 프로그램에서 데이터 소스를 만드는 방법에 대 한 자세한 내용은 [Microsoft Office에서 Visual FoxPro 데이터에 액세스](../../odbc/microsoft/accessing-visual-foxpro-data-from-microsoft-office.md)를 참조 하세요.  
  
### <a name="to-add-a-visual-foxpro-data-source"></a>Visual FoxPro 데이터 원본을 추가 하려면  
  
1.  Windows 2000를 실행 하는 컴퓨터에서 Windows 제어판을 열고 관리 도구를 두 번 클릭 합니다.  
  
2.  데이터 원본 (ODBC)을 두 번 클릭 하 여 ODBC 데이터 원본 관리자 대화 상자를 엽니다. 이 아이콘은 Visual FoxPro ODBC 드라이버 또는 ODBC 드라이버 소프트웨어를 설치한 후에 사용할 수 있습니다.  
  
    > [!NOTE]  
    >  이전 버전의 Windows를 실행 하는 경우 Windows 제어판을 열고 32 비트 ODBC 또는 ODBC를 두 번 클릭 하 여 ODBC 데이터 원본 관리자 대화 상자를 엽니다.  
  
3.  추가를 클릭합니다.  
  
4.  새 데이터 소스 만들기 대화 상자에서 Microsoft Visual FoxPro 드라이버를 선택한 다음 마침을 클릭 합니다.  
  
5.  [ODBC Visual FoxPro 설정 대화 상자](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)에서 데이터 원본 이름 및 설명을 입력 하 고 데이터베이스 유형을 선택한 다음 데이터베이스 또는 디렉터리를 선택 하 고 확인을 클릭 합니다.  
  
     ODBC 데이터 원본 관리자 대화 상자의 사용자 DSN 탭에 있는 사용자 데이터 원본 목록에 새 데이터 원본 이름이 표시 됩니다.  
  
6.  확인을 클릭 하 여 새 데이터 원본을 저장 하 고 ODBC 데이터 원본 관리자 대화 상자를 닫습니다.
