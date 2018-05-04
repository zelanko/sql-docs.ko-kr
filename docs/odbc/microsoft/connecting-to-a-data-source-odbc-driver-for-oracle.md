---
title: 데이터 원본 (ODBC Driver for Oracle)에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connecting to data source [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connecting to data sources
ms.assetid: f724a9c5-342a-4f4e-a030-ec34f7378eaf
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ff9f7ab2cb1510309a7822cad5f2943d1c131ece
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>데이터 원본 (ODBC Driver for Oracle)에 연결
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. Oracle에서 제공 하는 ODBC 드라이버를 사용 하십시오.  
  
 ODBC 응용 프로그램에 다양 한 방법으로 연결 정보를 전달할 수 있습니다. 예를 들어 응용 프로그램에는 항상 사용자에 게 연결 정보를 확인 하는 드라이버가 있을 수 있습니다. 또는 응용 프로그램 데이터 원본 연결을 지정 하는 연결 문자열을 예상할 수 있습니다. 데이터 원본에 연결 하는 방법을 ODBC 응용 프로그램에서 사용 하는 연결 방법에 따라 달라 집니다.  
  
 데이터 원본에 연결 하는 데 하나의 일반적인 방법은 데이터 원본 대화 상자를 통해입니다. ODBC 응용 프로그램 대화 상자를 사용 하도록 설치 되 면 대화 상자를 표시 되 고 메시지는 적절 한 데이터 원본 연결 정보를 표시 합니다.  
  
 사용 하 여 데이터 원본에 연결할 수도 있습니다는 [연결 문자열](../../odbc/microsoft/connection-string-format-and-attributes.md)합니다.  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>대화 상자를 사용 하 여 데이터 원본에 연결 하려면  
  
1.  데이터 원본 대화 상자에 표시 되 면 Oracle 데이터 원본을 선택한 다음 확인을 클릭 합니다. 연결 대화 상자가 나타납니다.  
  
2.  연결 대화 상자에 대 한 적절 한 정보 입력 한 다음 확인을 누릅니다.  
  
 연결 후 응용 프로그램 Oracle에 대 한 ODBC 드라이버를 사용 하 여 데이터 원본에 포함 된 정보에 액세스할 수 정보 확인 됩니다.
