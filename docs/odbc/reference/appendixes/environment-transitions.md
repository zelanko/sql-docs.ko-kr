---
title: 환경 전환 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment transitions [ODBC]
- transitioning states [ODBC], environment
- state transitions [ODBC], environment
ms.assetid: 9d11b1ab-f4c8-48ca-9812-8c04303f939d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6b1de2f2147357f9e2ed4f71657b9298c4a13684
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67910430"
---
# <a name="environment-transitions"></a>환경 전환
ODBC 환경에는 다음과 같은 세 가지 상태가 있습니다.  
  
|시스템 상태|Description|  
|-----------|-----------------|  
|E0|할당 되지 않은 환경|  
|E1|할당 된 환경, 할당 되지 않은 연결|  
|E2|할당 된 환경, 할당 된 연결|  
  
 다음 표에서는 각 ODBC 함수가 환경 상태에 미치는 영향을 보여 줍니다.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> 할당할|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|E1 [1]|--[4]|--[4]|  
|항목 sr-2|E2 [5]<br />HY010 6|--[4]|  
|항목 3|항목|--[4]|  
  
 [1] *HandleType* 가 SQL_HANDLE_ENV 된 경우이 행은 전환을 표시 합니다.  
  
 [2] *HandleType* 가 SQL_HANDLE_DBC 된 경우이 행은 전환을 표시 합니다.  
  
 [3] *HandleType* 가 SQL_HANDLE_STMT 또는 SQL_HANDLE_DESC 경우이 행은 전환을 표시 합니다.  
  
 [4] 올바른 핸들을 가리키는 *OutputHandlePtr* 로 **SQLAllocHandle** 를 호출 하면 해당 핸들이 덮어쓰여집니다. 이는 응용 프로그램 프로그래밍 오류 일 수 있습니다.  
  
 [5] 환경에 SQL_ATTR_ODBC_VERSION 환경 특성이 설정 되었습니다.  
  
 [6] 환경에 SQL_ATTR_ODBC_VERSION 환경 특성이 설정 되지 않았습니다.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources 원본 및 Sqldatasources  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> 할당할|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|항목|--[1]<br />HY010 sr-2|--[1]<br />HY010 sr-2|  
  
 [1] 환경에 SQL_ATTR_ODBC_VERSION 환경 특성이 설정 되었습니다.  
  
 [2] 환경에 SQL_ATTR_ODBC_VERSION 환경 특성이 설정 되지 않았습니다.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> 할당할|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|항목 비슷합니다|--[3]<br />HY010 3-4|--[3]<br />HY010 3-4|  
|항목 sr-2|항목|--|  
  
 [1] *HandleType* 가 SQL_HANDLE_ENV 된 경우이 행은 전환을 표시 합니다.  
  
 [2] *HandleType* 가 SQL_HANDLE_DBC 된 경우이 행은 전환을 표시 합니다.  
  
 [3] 환경에 SQL_ATTR_ODBC_VERSION 환경 특성이 설정 되었습니다.  
  
 [4] 환경에 SQL_ATTR_ODBC_VERSION 환경 특성이 설정 되지 않았습니다.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> 할당할|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|항목 비슷합니다|E0|HY010|  
|항목 sr-2|항목|--[4]<br />E1 [5]|  
|항목 3|항목|--|  
  
 [1] *HandleType* 가 SQL_HANDLE_ENV 된 경우이 행은 전환을 표시 합니다.  
  
 [2] *HandleType* 가 SQL_HANDLE_DBC 된 경우이 행은 전환을 표시 합니다.  
  
 [3] *HandleType* 가 SQL_HANDLE_STMT 또는 SQL_HANDLE_DESC 경우이 행은 전환을 표시 합니다.  
  
 [4] 다른 할당 된 연결 핸들이 있습니다.  
  
 [5] *핸들* 에 지정 된 연결 핸들이 유일 하 게 할당 된 연결 핸들 이었습니다.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField 및 SQLGetDiagRec  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> 할당할|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|항목 비슷합니다|--|--|  
|항목 sr-2|항목|--|  
  
 [1] *HandleType* 가 SQL_HANDLE_ENV 된 경우이 행은 전환을 표시 합니다.  
  
 [2] *HandleType* 가 SQL_HANDLE_DBC, SQL_HANDLE_STMT 또는 SQL_HANDLE_DESC 된 경우이 행은 전환을 표시 합니다.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> 할당할|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|항목|--[1]<br />HY010 sr-2|--|  
  
 [1] 환경에 SQL_ATTR_ODBC_VERSION 환경 특성이 설정 되었습니다.  
  
 [2] 환경에 SQL_ATTR_ODBC_VERSION 환경 특성이 설정 되지 않았습니다.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> 할당할|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|항목|--[1]<br />HY010 sr-2|HY011|  
  
 [1] 환경에 SQL_ATTR_ODBC_VERSION 환경 특성이 설정 되었습니다.  
  
 [2] *특성* 인수가 SQL_ATTR_ODBC_VERSION 되지 않고 환경에 SQL_ATTR_ODBC_VERSION 환경 특성이 설정 되지 않았습니다.  
  
## <a name="all-other-odbc-functions"></a>기타 모든 ODBC 함수  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> 할당할|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|항목|항목|--|
