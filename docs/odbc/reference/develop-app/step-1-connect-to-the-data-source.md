---
title: '1단계: 데이터 원본에 연결 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], connecting to data source
- data sources [ODBC], connections
- connecting to data source [ODBC], steps
ms.assetid: 84298664-4523-4149-b821-7b2e42c85281
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 154fdd7368835ba2a578d3ec641705c4064859ac
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149015"
---
# <a name="step-1-connect-to-the-data-source"></a>1단계: 데이터 원본에 연결
첫 번째 단계는 모든 응용 프로그램 데이터 원본에 연결 하는 것입니다. 필요한 함수를 포함 하 여이 단계는 다음 그림에 표시 됩니다.  
  
 ![ODBC 응용 프로그램에서 데이터 원본에 연결할](../../../odbc/reference/develop-app/media/pr11.gif "pr11")  
  
 데이터 원본에 연결 하는 첫 번째 단계는 드라이버 관리자를 로드 하 고 사용 하 여 환경 핸들을 할당 하는 것 **SQLAllocHandle**합니다. 자세한 내용은 [환경 핸들 할당](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)합니다.  
  
 그런 다음 응용 프로그램 호출 하 여 준수 하는 ODBC의 버전을 등록 **SQLSetEnvAttr** SQL_ATTR_APP_ODBC_VER 환경 특성을 사용 합니다. 자세한 내용은 [응용 프로그램의 ODBC 버전 선언](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) 하 고 [이전 버전과 호환성 및 표준 준수](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)합니다.  
  
 응용 프로그램에서 사용 하 여 연결 핸들을 할당 하는 어 **SQLAllocHandle** 사용 하 여 데이터 원본에 연결 하 고 **SQLConnect**, **SQLDriverConnect**, 또는 **SQLBrowseConnect**합니다. 자세한 내용은 [연결 핸들 할당](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md) 하 고 [연결](../../../odbc/reference/develop-app/establishing-a-connection.md)합니다.  
  
 그러면 응용 프로그램이 트랜잭션을 수동으로 커밋 여부와 같은 모든 연결 특성을 설정 합니다. 자세한 내용은 [연결 특성](../../../odbc/reference/develop-app/connection-attributes.md)합니다.
