---
title: Installer DLL API Reference 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installer DLL [ODBC]
ms.assetid: 47fcadc3-f102-4989-9ee7-a1c65233142a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 14a89c859e98a069106b79c9289187a64c310fa9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63232812"
---
# <a name="installer-dll-api-reference-function"></a>설치 관리자 DLL API 참조 함수
이 섹션의 설치 관리자 DLL API 함수 구문을 설명합니다. Installer DLL API 함수를 20으로 이루어져 있습니다. 이러한 함수의 세 **SQLGetTranslator**를 **SQLRemoveDSNFromIni**, 및 **SQLWriteDSNToIni**, Dll 설정 의해서만 호출 됩니다. 다른 함수를 설치 및 관리 프로그램에 의해 호출 됩니다.  
  
 각 함수는 도입 하는 ODBC의 버전을 사용 하 여 레이블이 지정 됩니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [SQLConfigDataSource 함수](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)  
  
-   [SQLConfigDriver 함수](../../../odbc/reference/syntax/sqlconfigdriver-function.md)  
  
-   [SQLCreateDataSource 함수](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)  
  
-   [SQLGetConfigMode 함수](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)  
  
-   [SQLGetInstalledDrivers 함수](../../../odbc/reference/syntax/sqlgetinstalleddrivers-function.md)  
  
-   [SQLGetPrivateProfileString 함수](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)  
  
-   [SQLGetTranslator 함수](../../../odbc/reference/syntax/sqlgettranslator-function.md)  
  
-   [SQLInstallDriverEx 함수](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)  
  
-   [SQLInstallDriverManager 함수](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)  
  
-   [SQLInstallerError 함수](../../../odbc/reference/syntax/sqlinstallererror-function.md)  
  
-   [SQLInstallTranslator 함수](../../../odbc/reference/syntax/sqlinstalltranslator-function.md)  
  
-   [SQLInstallTranslatorEx 함수](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)  
  
-   [SQLManageDataSources 함수](../../../odbc/reference/syntax/sqlmanagedatasources.md)  
  
-   [SQLPostInstallerError 함수](../../../odbc/reference/syntax/sqlpostinstallererror-function.md)  
  
-   [SQLReadFileDSN 함수](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)  
  
-   [SQLRemoveDefaultDataSource 함수](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)  
  
-   [SQLRemoveDriver 함수](../../../odbc/reference/syntax/sqlremovedriver-function.md)  
  
-   [SQLRemoveDriverManager 함수](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)  
  
-   [SQLRemoveDSNFromIni 함수](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)  
  
-   [SQLRemoveTranslator 함수](../../../odbc/reference/syntax/sqlremovetranslator-function.md)  
  
-   [SQLSetConfigMode 함수](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)  
  
-   [SQLValidDSN 함수](../../../odbc/reference/syntax/sqlvaliddsn-function.md)  
  
-   [SQLWriteDSNToIni 함수](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)  
  
-   [SQLWriteFileDSN 함수](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)  
  
-   [SQLWritePrivateProfileString 함수](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)
