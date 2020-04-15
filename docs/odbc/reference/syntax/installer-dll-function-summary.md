---
title: 설치 프로그램 DLL 기능 요약 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], installer DLL functions
- installer DLL [ODBC]
ms.assetid: 666c09d3-1e10-4d89-9b42-eda2957a87f0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ddaf20334a84833433961a49e17724d354945c5a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298773"
---
# <a name="installer-dll-function-summary"></a>설치 관리자 DLL 함수 요약
다음 표에서는 설치 관리자 DLL의 함수에 대해 설명합니다. 각 함수에 대한 구문 및 의미 체계에 대한 자세한 내용은 [설치 관리자 DLL API 참조를](../../../odbc/reference/syntax/installer-dll-api-reference-function.md)참조하십시오.  
  
|Task|함수 이름|용도|  
|----------|-------------------|-------------|  
|ODBC 설치|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|드라이버별 설정 DLL을 로드합니다.|  
||[SQLGetInstalled드라이버](../../../odbc/reference/syntax/sqlgetinstalleddrivers-function.md)|설치된 드라이버 목록을 반환합니다.|  
||[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|시스템 정보에 드라이버를 추가합니다.|  
||[SQLInstallDriver관리자](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|드라이버 관리자에 대 한 대상 디렉터리를 반환 합니다.|  
||[SQLInstaller오류](../../../odbc/reference/syntax/sqlinstallererror-function.md)|설치 관리자 기능에 대한 오류 또는 상태 정보를 반환합니다.|  
||[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|시스템 정보에 번역기를 추가합니다.|  
||[SQL포스트설치자 오류](../../../odbc/reference/syntax/sqlpostinstallererror-function.md)|드라이버 또는 번역기 설치 라이브러리에서 오류를 보고할 수 있습니다.|  
||[SQLRemove드라이버](../../../odbc/reference/syntax/sqlremovedriver-function.md)|시스템 정보에서 드라이버를 제거합니다.|  
||[SQLRemove드라이버관리자](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|시스템 정보에서 ODBC 핵심 구성 요소를 제거합니다.|  
||[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|시스템 정보에서 번역기를 제거합니다.|  
|데이터 원본 구성|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|드라이버 별 설정 DLL을 호출합니다.|  
||[SQLCreate데이터 소스](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|데이터 원본을 추가하는 대화 상자를 표시합니다.|  
||[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|DSN 값을 나열하는 Odbc.ini 항목이 시스템 정보에 있는 위치를 나타내는 구성 모드를 검색합니다.|  
||[SQLGet개인 프로필 스트링](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|시스템 정보에 값을 씁니다.|  
||[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|번역기를 선택하는 대화 상자를 표시합니다.|  
||[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|데이터 원본 및 드라이버를 구성하는 대화 상자를 표시합니다.|  
||[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|파일 DSN에서 정보를 읽습니다.|  
||[SQLRemoveDefault데이터 소스](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|기본 데이터 원본을 제거합니다.|  
||[SQLRemoveDSNIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|데이터 원본을 제거합니다.|  
||[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|시스템 정보에 DSN 값을 나열하는 Odbc.ini 항목의 위치를 나타내는 구성 모드를 설정합니다.|  
||[SQLValidDSN](../../../odbc/reference/syntax/sqlvaliddsn-function.md)|데이터 원본 이름의 길이와 유효성을 확인합니다.|  
||[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|데이터 원본을 추가합니다.|  
||[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|DSN 파일에 정보를 씁니다.|  
||[SQLWrite개인 프로필 스트링](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|시스템 정보에서 값을 가져옵니다.|
