---
title: "데이터베이스 속성(변경 내용 추적 페이지) | Microsoft 문서"
ms.custom: 
ms.date: 01/07/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.databaseproperties.changetracking.f1
ms.assetid: 9b929640-bc62-449b-9b06-b5a77b8cf372
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2aab898a267244d585d1d09bc66eaca4814895a1
ms.lasthandoff: 04/11/2017

---
# <a name="database-properties-changetracking-page"></a>데이터베이스 속성(변경 내용 추적 페이지)
  이 페이지를 사용하여 선택한 데이터베이스의 변경 내용 추적 설정을 확인하거나 수정할 수 있습니다. 이 페이지에서 사용할 수 있는 옵션에 대한 자세한 내용은 [변경 내용 추적 설정 및 해제&#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)를 참조하세요.  
  
## <a name="options"></a>옵션  
 **변경 내용 추적**  
 데이터베이스에 대해 변경 내용 추적을 설정하거나 해제하는 데 사용합니다.  
  
 변경 내용 추적을 설정하려면 데이터베이스를 수정할 수 있는 권한이 있어야 합니다.  
  
 값을 **True** 로 설정하면 개별 테이블에 변경 내용 추적을 사용하는 데이터베이스 옵션이 설정됩니다.  
  
 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)를 사용하여 변경 내용 추적을 구성할 수도 있습니다.  
  
 **보존 기간**  
 데이터베이스에 변경 내용 추적 정보를 보존하는 최소 기간을 지정합니다. 데이터는 **자동 정리**값이 **True**인 경우에만 제거됩니다.  
  
 기본값은 2입니다.  
  
 **보존 기간 단위**  
 보존 기간 값의 단위를 지정합니다. **일**, **시간**또는 **분**을 선택할 수 있습니다. 기본값은 **일**입니다.  
  
 최소 보존 기간은 1분입니다. 최대 보존 기간은 없습니다.  
  
 **자동 정리**  
 지정된 보존 기간 후에 변경 내용 추적 정보가 자동으로 제거되는지 여부를 나타냅니다.  
  
 **자동 정리** 를 설정하면 이전의 모든 사용자 지정 보존 기간이 기본 보존 기간인 2일로 다시 설정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
  

