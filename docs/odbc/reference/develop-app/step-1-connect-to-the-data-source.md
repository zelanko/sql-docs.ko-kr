---
title: '1 단계: 데이터 원본에 연결 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], connecting to data source
- data sources [ODBC], connections
- connecting to data source [ODBC], steps
ms.assetid: 84298664-4523-4149-b821-7b2e42c85281
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 98fff3a58b7bc191b275d4f887f5856700f7fa91
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915608"
---
# <a name="step-1-connect-to-the-data-source"></a>1 단계: 데이터 원본에 연결
첫 번째 단계는 응용 프로그램에서 데이터 원본에 연결 하는 것입니다. 필요한 함수를 포함 하 여이 단계는 다음 그림에 표시 됩니다.  
  
 ![ODBC 응용 프로그램에서 데이터 원본에 연결할](../../../odbc/reference/develop-app/media/pr11.gif "pr11")  
  
 드라이버 관리자를 로드 하 고 있는 환경 핸들을 할당 하는 데이터 원본에 연결 하는 첫 번째 단계는 **SQLAllocHandle**합니다. 자세한 내용은 참조 [환경 처리할 할당](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)합니다.  
  
 그런 다음 응용 프로그램을 호출 하 여 준수 하는 ODBC의 버전 등록 **SQLSetEnvAttr** SQL_ATTR_APP_ODBC_VER 환경 특성을 사용 합니다. 자세한 내용은 참조 [응용 프로그램의 ODBC 버전 선언](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) 및 [이전 버전과 호환성 및 표준 준수](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)합니다.  
  
 응용 프로그램으로 연결 핸들을 할당 하는 다음으로, **SQLAllocHandle** 사용 하 여 데이터 소스에 연결 되어 **SQLConnect**, **SQLDriverConnect**, 또는 **SQLBrowseConnect**합니다. 자세한 내용은 참조 [연결 핸들 할당](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md) 및 [연결을 설정](../../../odbc/reference/develop-app/establishing-a-connection.md)합니다.  
  
 그런 다음 응용 프로그램에 트랜잭션을 수동으로 커밋하려면 여부와 같은 연결 특성을 설정 합니다. 자세한 내용은 참조 [연결 특성](../../../odbc/reference/develop-app/connection-attributes.md)합니다.
