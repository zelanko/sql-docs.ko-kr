---
description: SQLGetInstalledDrivers 함수
title: SQLGetInstalledDrivers 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetInstalledDrivers
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetInstalledDrivers
helpviewer_keywords:
- SQLGetInstalledDrivers function [ODBC]
ms.assetid: a1983a2e-0edf-422e-bd1b-ec5db40a34bc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0599cb187dee9d3b860f619538b1e0dc148ad58d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421267"
---
# <a name="sqlgetinstalleddrivers-function"></a>SQLGetInstalledDrivers 함수
**규칙**  
 소개 된 버전: ODBC 1.0  
  
 **요약**  
 **SQLGetInstalledDrivers** 는 시스템 정보의 [ODBC Drivers] 섹션을 읽고 설치 된 드라이버에 대 한 설명 목록을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLGetInstalledDrivers(  
     LPSTR   lpszBuf,  
     WORD    cbBufMax,  
     WORD *  pcbBufOut);  
```  
  
## <a name="arguments"></a>인수  
 *lpszBuf*  
 출력 설치 된 드라이버에 대 한 설명 목록입니다. 목록 구조에 대 한 자세한 내용은 "Comments"를 참조 하십시오.  
  
 *cbBufMax*  
 입력 *LpszBuf*의 길이입니다.  
  
 *pcbBufOut*  
 출력 *LpszBuf*에 반환 된 총 바이트 수입니다 (null 종결 바이트 제외). 반환할 수 있는 바이트 수가 *Cbbufmax*보다 크거나 같으면 *lpszBuf* 의 드라이버 설명 목록이 *cbbufmax* 에서 null 종료 문자를 뺀 값으로 잘립니다. *Pcbbufout* 인수는 null 포인터 일 수 있습니다.  
  
## <a name="returns"></a>반환  
 이 함수는 성공 하면 TRUE를 반환 하 고 실패 하면 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetInstalledDrivers** 가 FALSE를 반환 하면 **SQLInstallerError**을 호출 하 여 연결 된 * \* pfErrorCode* 값을 얻을 수 있습니다. 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \* pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|오류|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생 했습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못 된 버퍼 길이|*LpszBuf* 인수가 NULL 이거나 잘못 되었거나, *Cbbufmax* 인수가 0 보다 작거나 같습니다.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|레지스트리에서 구성 요소를 찾을 수 없음|레지스트리에서 [ODBC Drivers] 섹션을 찾을 수 없습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리가 부족 하 여 설치 관리자가 함수를 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 각 드라이버 설명은 null 바이트로 종료 되 고 전체 목록은 null 바이트로 종료 됩니다. 즉, 두 개의 null 바이트가 목록의 끝을 표시 합니다. 할당 된 버퍼가 전체 목록을 저장할 만큼 크지 않은 경우 목록이 오류 없이 잘립니다. Null 포인터가 *lpszBuf*로 전달 되 면 오류가 반환 됩니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|드라이버 설명 및 특성 반환|[SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|
