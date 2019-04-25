---
title: Microsoft Access로 Visual FoxPro 데이터 가져오기 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f19b58ba93c94088c4cae19f1093d89c8decb843
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62471304"
---
# <a name="importing-visual-foxpro-data-into-microsoft-access"></a>Microsoft Access로 Visual FoxPro 데이터 가져오기
Visual FoxPro 데이터베이스 가져오기 옵션을 사용 하 여 Microsoft Access 데이터베이스에 저장 된 데이터를 가져올 수 있습니다.  
  
### <a name="to-import-visual-foxpro-data-into-a-microsoft-access-database"></a>Visual FoxPro 데이터는 Microsoft Access 데이터베이스를 가져오려면  
  
1.  Microsoft Access 데이터베이스를 엽니다.  
  
2.  파일 메뉴에서 외부 데이터 가져오기 가져와서를 선택 합니다.  
  
3.  가져오기 대화 상자에서 파일 형식 목록에서에서 ODBC 데이터베이스를 선택 합니다.  
  
4.  SQL 데이터 원본 대화 상자에서 클릭 하 고 쿼리 하려는 FoxPro 데이터에 연결 하는 Visual FoxPro 데이터 소스를 선택 합니다.  
  
5.  개체 가져오기 대화 상자에서 확인 클릭 하려는 하나 이상의 테이블을 선택 합니다. 가져온 Visual FoxPro 테이블의 이름은 Microsoft Access 데이터베이스의 테이블 탭에 표시 됩니다.  
  
 이제 가져온된 Visual FoxPro 테이블의 데이터를 조작 하 여 Microsoft Access를 사용할 수 있습니다. 가져오는 데이터는 Visual FoxPro;에 저장 된 데이터의 스냅숏입니다. 가져온된 데이터를 변경한 Visual FoxPro 데이터 원본에 다시 전송 되지 않습니다.  
  
 Visual FoxPro 데이터 원본에서 데이터를 변경 하려면 참조는 Microsoft Access에서 수행한 변경 내용을 [쿼리 및 Microsoft Access에서 Visual FoxPro 데이터 업데이트](../../odbc/microsoft/querying-and-updating-visual-foxpro-data-from-microsoft-access.md)합니다.
