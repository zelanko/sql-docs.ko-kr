---
title: SQLInstallTranslator 매핑 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLInstallTranslator function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLInstallTranslator
ms.assetid: bcd9ba4f-7834-4bc4-876e-c7478998e524
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ab5ebccaac7ccf6374971c1d21040ad15fb3e55
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300585"
---
# <a name="sqlinstalltranslator-mapping"></a>SQLInstallTranslator 매핑
ODBC *2.x* 응용 프로그램이 ODBC *3.x* 드라이버를 통해 **SQLInstallTranslator를** 호출하면 드라이버 관리자는 **SQLInstallTranslatorEx에**대한 호출을 매핑합니다. 응용 프로그램은 *LPszInfFile* 인수가 NULL 이외의 값으로 설정된 ODBC *3.x* 드라이버 관리자에서 **SQLInstallTranslator를** 호출해서는 안 됩니다. The ODBC. ODBC *2.x에* 사용되는 INF 파일은 이전 버전과의 호환성에서도 ODBC *3.x에서*더 이상 지원되지 않습니다.
