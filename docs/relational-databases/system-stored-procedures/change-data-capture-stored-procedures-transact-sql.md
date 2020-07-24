---
title: 변경 데이터 캡처 저장 프로시저 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system stored procedures [SQL Server], change data capture
- change data capture [SQL Server], stored procedures
ms.assetid: 7da7068d-6388-465a-b708-a2f27ded1efe
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a0d5f3f10f20fb5489760a1e415309dcfd01482e
ms.sourcegitcommit: 08f331b6a5fe72d68ef1b2eccc5d16cb80c6ee39
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86977634"
---
# <a name="change-data-capture-stored-procedures-transact-sql"></a>변경 데이터 캡처 저장 프로시저(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  변경 데이터 캡처는 설정된 테이블에서 발생한 DML(데이터 조작 언어) 작업의 기록 레코드를 편리한 관계형 형식으로 사용할 수 있게 합니다. 다음 저장 프로시저를 사용하여 변경 데이터 캡처를 구성하고, 변경 데이터 캡처 에이전트 작업을 관리하고, 변경 데이터 소비자에 현재 메타데이터를 제공할 수 있습니다.  

:::row:::
    :::column:::
        [sys.sp_cdc_add_job&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)

        [sp_cdc_change_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md)

        [sp_cdc_cleanup_change_table &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-cleanup-change-table-transact-sql.md)

        [sp_cdc_disable_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md)

        [sp_cdc_disable_table &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-table-transact-sql.md)

        [sp_cdc_drop_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-drop-job-transact-sql.md)

        [sp_cdc_enable_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md)

        [sp_cdc_enable_table &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)
    :::column-end:::
    :::column:::
        [sp_cdc_generate_wrapper_function &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)

        [sp_cdc_get_captured_columns &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md)

        [sp_cdc_get_ddl_history &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md)

        [sp_cdc_help_change_data_capture &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)

        [sp_cdc_help_jobs &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)

        [sp_cdc_scan &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md)

        [sp_cdc_start_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-start-job-transact-sql.md)

        [sp_cdc_stop_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-stop-job-transact-sql.md)
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목  
 [변경 데이터 캡처 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/change-data-capture-tables-transact-sql.md)  
  
  
