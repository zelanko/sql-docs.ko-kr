---
title: 마이크로 소프트 액세스로 비주얼 폭스 프로 데이터를 가져 오기 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], Access
- Visual FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], importing
ms.assetid: a3591295-0a76-4e3c-b4fa-8bd4f1cde705
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 90ac16bbdbaf7f4dd29e14e66cf5b9dc666057f4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302454"
---
# <a name="importing-visual-foxpro-data-into-microsoft-access"></a>Microsoft Access로 Visual FoxPro 데이터 가져오기
가져오기 옵션을 사용하여 Visual FoxPro 데이터베이스에 저장된 데이터를 Microsoft Access 데이터베이스로 가져올 수 있습니다.  
  
### <a name="to-import-visual-foxpro-data-into-a-microsoft-access-database"></a>비주얼 FoxPro 데이터를 Microsoft 액세스 데이터베이스로 가져오려면  
  
1.  Microsoft 액세스 데이터베이스를 엽니다.  
  
2.  파일 메뉴에서 외부 데이터 가져오기를 선택한 다음 가져오기를 선택합니다.  
  
3.  가져오기 대화 상자에서 형식 목록의 파일에서 ODBC 데이터베이스를 선택합니다.  
  
4.  SQL 데이터 원본 대화 상자에서 쿼리하려는 FoxPro 데이터에 연결하는 Visual FoxPro 데이터 원본을 선택하고 확인을 클릭합니다.  
  
5.  개체 가져오기 대화 상자에서 가져올 테이블을 하나 이상 선택하고 확인을 클릭합니다. 가져온 Visual FoxPro 테이블의 이름은 Microsoft Access 데이터베이스의 테이블 탭에 표시됩니다.  
  
 이제 Microsoft Access를 사용하여 가져온 Visual FoxPro 테이블의 데이터를 조작할 수 있습니다. 가져오는 데이터는 Visual FoxPro에 저장된 데이터의 스냅샷입니다. 가져온 데이터에 대한 변경 내용은 Visual FoxPro 데이터 원본으로 다시 전송되지 않습니다.  
  
 Microsoft Access에서 변경하여 Visual FoxPro 데이터 원본의 데이터를 변경하려면 [Microsoft Access에서 시각적 FoxPro 데이터 쿼리 및 업데이트](../../odbc/microsoft/querying-and-updating-visual-foxpro-data-from-microsoft-access.md)를 참조하십시오.
