---
title: '1 단계: 데이터 원본에 연결 | Microsoft Docs'
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
ms.openlocfilehash: 80f2dfc05d9d27f60aca414ee0abd13e13b3ea65
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114265"
---
# <a name="step-1-connect-to-the-data-source"></a>1단계: 데이터 원본에 연결
모든 응용 프로그램의 첫 번째 단계는 데이터 원본에 연결 하는 것입니다. 이 단계는 필요한 함수를 포함 하 여 다음 그림에 나와 있습니다.  
  
 ![ODBC 응용 프로그램의 데이터 소스에 연결](../../../odbc/reference/develop-app/media/pr11.gif "pr11")  
  
 데이터 원본에 연결 하는 첫 번째 단계는 드라이버 관리자를 로드 하 고 **SQLAllocHandle**를 사용 하 여 환경 핸들을 할당 하는 것입니다. 자세한 내용은 [환경 핸들 할당](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)을 참조 하세요.  
  
 그런 다음 SQL_ATTR_APP_ODBC_VER 환경 특성을 사용 하 여 **SQLSetEnvAttr** 를 호출 하 여 해당 응용 프로그램이 준수 하는 ODBC 버전을 등록 합니다. 자세한 내용은 [응용 프로그램의 ODBC 버전 선언](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) 및 [이전 버전과의 호환성 및 표준 준수](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)를 참조 하세요.  
  
 그런 다음 응용 프로그램은 **SQLAllocHandle** 를 사용 하 여 연결 핸들을 할당 하 고 **SQLConnect**, **SQLDriverConnect**또는 **SQLBrowseConnect**를 사용 하 여 데이터 원본에 연결 합니다. 자세한 내용은 [연결 핸들 할당](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md) 및 [연결 설정](../../../odbc/reference/develop-app/establishing-a-connection.md)을 참조 하세요.  
  
 그런 다음 응용 프로그램은 수동으로 트랜잭션을 커밋하는 지 여부와 같은 모든 연결 특성을 설정 합니다. 자세한 내용은 [연결 특성](../../../odbc/reference/develop-app/connection-attributes.md)을 참조 하세요.
