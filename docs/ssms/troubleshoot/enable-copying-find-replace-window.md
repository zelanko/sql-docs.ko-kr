---
description: '찾기 및 바꾸기 창에서 복사를 사용하기 위한 해결 방법 '
title: 찾기 및 바꾸기 창에서 복사 사용
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan, sstein
ms.custom: seo-lt-2019
ms.date: 11/03/2020
ms.openlocfilehash: ea5ae3f9fa941e723d3bdf10de0ec900310cc28d
ms.sourcegitcommit: 985e2e8e494badeac6d6b652cd35765fd9c12d80
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/04/2020
ms.locfileid: "93328783"
---
# <a name="workaround-to-enable-copying-from-find-and-replace-window"></a>찾기 및 바꾸기 창에서 복사를 사용하기 위한 해결 방법

[!INCLUDE[Applies to](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

찾기 및 바꾸기 창에서 복사를 사용하려면 해결 방법이 필요합니다.  SQL Server Management Studio의 찾기 및 바꾸기 창에서 복사할 수 없는 경우 아래 [해결 방법](#workaround)을 따르세요.

## <a name="error-message"></a>오류 메시지

SQL Server Management Studio의 찾기 및 바꾸기 창에서 텍스트를 복사하려고 하면 오류 메시지가 표시됩니다.

> 저장되지 않은 문서는 기타 파일 프로젝트에서 잘라내거나 클립보드로 복사할 수 없습니다. 저장되지 않은 문서를 잘라내거나 복사하기 전에 저장해야 합니다.

![다음의 오류 대화 상자: 저장되지 않은 문서는 기타 파일 프로젝트에서 잘라내거나 클립보드로 복사할 수 없습니다. 저장되지 않은 문서를 잘라내거나 복사하기 전에 저장해야 합니다.](../media/troubleshoot/unable-copy-find-replace-window.png)

## <a name="workaround"></a>해결 방법

찾기 및 바꾸기 창에서 텍스트 복사를 사용하도록 설정하려면 다음 단계를 수행합니다.

1. **도구** 메뉴에서 **옵션** 을 엽니다.

2. **환경**>**문서** 에서 “솔루션 탐색기에 기타 파일 표시” 항목의 선택을 취소합니다.

3. SQL Server Management Studio를 닫고 다시 엽니다.

![“솔루션 탐색기에 기타 파일 표시”가 선택되지 않은 옵션 창](../media/troubleshoot/fix-copy-find-replace-window.png)

