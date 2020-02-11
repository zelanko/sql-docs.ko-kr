---
title: Visual FoxPro 데이터베이스에서 Microsoft Excel로 데이터 가져오기 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Excel
- Visual FoxPro data [ODBC], Excel
- Visual FoxPro data [ODBC], importing
- Visual FoxPro ODBC driver [ODBC], Excel
ms.assetid: 3085bc4c-00a7-40e5-bffb-c3962cd3d509
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3c65635132c5f98b0565391122877f2e3c0a6714
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085554"
---
# <a name="importing-data-into-microsoft-excel-from-a-visual-foxpro-database"></a>Visual FoxPro 데이터베이스에서 Microsoft Excel로 데이터 가져오기
데이터 원본을 정의한 경우 Visual FoxPro 데이터를 Microsoft Excel 워크시트로 가져올 수 있습니다. Visual FoxPro 데이터 원본을 만드는 방법에 대 한 자세한 내용은 [Microsoft Excel에서 Visual Foxpro 데이터 원본에 액세스](../../odbc/microsoft/accessing-a-visual-foxpro-data-source-from-microsoft-excel.md)를 참조 하세요.  
  
### <a name="to-import-visual-foxpro-data-into-an-microsoft-excel-worksheet"></a>Microsoft Excel 워크시트로 Visual FoxPro 데이터를 가져오려면  
  
1.  Microsoft Excel 스프레드시트를 엽니다.  
  
2.  데이터 메뉴에서 외부 데이터 가져오기를 선택 합니다. Microsoft Query가 열립니다.  
  
3.  데이터 소스 선택 대화 상자에서 Visual FoxPro 데이터 원본을 선택한 다음 사용을 클릭 합니다.  
  
4.  데이터 원본에 의해 액세스 되는 데이터베이스에 테이블이 포함 되어 있는 경우 테이블 추가 대화 상자에서 테이블을 선택 합니다. Microsoft Query는 쿼리 디자이너의 위쪽 절반에 추가 된 테이블을 표시 합니다.  
  
    > [!NOTE]  
    >  소유자 목록은이 대화 상자에서 사용할 수 없습니다 .이는 드라이버가 소유자를 지원 하지 않기 때문입니다. 드라이버가 데이터 원본에서 여러 데이터베이스를 지원 하지 않으므로 데이터베이스 목록을 사용할 수 없습니다.  
  
5.  테이블에서 디자이너의 아래쪽으로 끌어서 놓는 방법으로 쿼리 필드를 선택 합니다.  
  
6.  Microsoft Query를 닫습니다. 선택한 데이터를 Microsoft Excel 스프레드시트로 가져옵니다.
