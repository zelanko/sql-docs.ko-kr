---
title: '1단계: 데이터 원본에 연결 | 마이크로 소프트 문서'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2a104733c0e5ec5acc87eeabd00c4e51d4bfd000
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301353"
---
# <a name="step-1-connect-to-the-data-source"></a>1단계: 데이터 원본에 연결
모든 응용 프로그램의 첫 번째 단계는 데이터 원본에 연결하는 것입니다. 필요한 함수를 포함하여 이 단계는 다음 그림에 나와 있습니다.  
  
 ![ODBC 응용 프로그램의 데이터 소스에 연결](../../../odbc/reference/develop-app/media/pr11.gif "pr11")  
  
 데이터 원본에 연결하는 첫 번째 단계는 드라이버 관리자를 로드하고 **SQLAllocHandle을**사용하여 환경 핸들을 할당하는 것입니다. 자세한 내용은 [환경 핸들 할당을](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)참조하십시오.  
  
 그런 다음 응용 프로그램은 **SQLSetEnvAttr을** SQL_ATTR_APP_ODBC_VER 환경 특성을 호출하여 준수하는 ODBC 버전을 등록합니다. 자세한 내용은 [응용 프로그램의 ODBC 버전 선언](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) 및 이전 버전 호환성 및 표준 [준수를](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)참조하십시오.  
  
 다음으로 응용 프로그램은 **SQLAllocHandle을** 사용하여 연결 핸들을 할당하고 **SQLConnect,** **SQLDriverConnect**또는 **SQLBrowseConnect**를 사용하여 데이터 원본에 연결합니다. 자세한 내용은 [연결 핸들 할당](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md) 및 연결 [설정](../../../odbc/reference/develop-app/establishing-a-connection.md)을 참조하십시오.  
  
 그런 다음 응용 프로그램은 트랜잭션을 수동으로 커밋할지 여부와 같은 연결 특성을 설정합니다. 자세한 내용은 [연결 특성 을](../../../odbc/reference/develop-app/connection-attributes.md)참조하십시오.
