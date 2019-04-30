---
title: 데이터 원본 (Oracle 용 ODBC 드라이버)에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to data source [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connecting to data sources
ms.assetid: f724a9c5-342a-4f4e-a030-ec34f7378eaf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: adee8d8dd8d6db0d79b37ff853c41e7604fe21de
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63302128"
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>데이터 원본에 연결(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신, Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 ODBC 응용 프로그램에서 다양 한 방법으로 연결 정보를 전달할 수 있습니다. 예를 들어, 응용 프로그램에는 항상 사용자에 게 연결 정보를 확인 하는 드라이버가 있을 수 있습니다. 또는 응용 프로그램 데이터 원본 연결을 지정 하는 연결 문자열을 예상 합니다. 데이터 원본에 연결 하는 방법을 ODBC 응용 프로그램에서 사용 되는 연결 방법에 따라 달라 집니다.  
  
 데이터 원본에 연결 하는 하나의 일반적인 방법은 데이터 원본 대화 상자를 통해 됩니다. ODBC 응용 프로그램은 대화 상자를 사용 하려면를 설정 하는 경우 해당 대화 상자 표시 되 고 적절 한 데이터 원본 연결 정보에 대 한 라는 메시지가 표시 됩니다.  
  
 사용 하 여 데이터 원본에 연결할 수도 있습니다는 [연결 문자열](../../odbc/microsoft/connection-string-format-and-attributes.md)합니다.  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>대화 상자를 사용 하 여 데이터 원본에 연결  
  
1.  데이터 원본 대화 상자에 표시 되 면 Oracle 데이터 소스를 선택 하 고 확인을 클릭 합니다. 연결 대화 상자가 나타납니다.  
  
2.  연결 대화 상자에 대 한 적절 한 정보를 입력 하 고 확인을 클릭 합니다.  
  
 연결 정보가 확인 되, 응용 프로그램 Oracle 용 ODBC 드라이버를 사용 하 여 데이터 원본에 포함 된 정보에 액세스할 수 있습니다.
