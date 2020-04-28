---
title: 데이터 원본에 연결 (Oracle 용 ODBC 드라이버) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6ef567c9e3c7b63e7f5044de699750de856f3e52
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81281303"
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>데이터 원본에 연결(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 ODBC 응용 프로그램은 여러 가지 방법으로 연결 정보를 전달할 수 있습니다. 예를 들어 응용 프로그램이 항상 사용자에 게 연결 정보를 입력 하 라는 메시지가 표시 될 수 있습니다. 또는 응용 프로그램에 데이터 원본 연결을 지정 하는 연결 문자열이 필요할 수 있습니다. 데이터 원본에 연결 하는 방법은 ODBC 응용 프로그램에서 사용 하는 연결 방법에 따라 달라 집니다.  
  
 데이터 원본에 연결 하는 일반적인 방법 중 하나는 데이터 원본 대화 상자를 통하는 것입니다. ODBC 응용 프로그램이 대화 상자를 사용 하도록 설정 된 경우 해당 대화 상자가 표시 되 고 적절 한 데이터 원본 연결 정보를 묻는 메시지가 표시 됩니다.  
  
 [연결 문자열](../../odbc/microsoft/connection-string-format-and-attributes.md)을 사용 하 여 데이터 원본에 연결할 수도 있습니다.  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>대화 상자를 사용 하 여 데이터 원본에 연결 하려면  
  
1.  데이터 원본 대화 상자가 나타나면 Oracle 데이터 원본을 선택 하 고 확인을 클릭 합니다. 연결 대화 상자가 나타납니다.  
  
2.  연결 대화 상자에 적절 한 정보를 입력 한 다음 확인을 클릭 합니다.  
  
 연결 정보를 확인 한 후 응용 프로그램은 Oracle 용 ODBC 드라이버를 사용 하 여 데이터 원본에 포함 된 정보에 액세스할 수 있습니다.
