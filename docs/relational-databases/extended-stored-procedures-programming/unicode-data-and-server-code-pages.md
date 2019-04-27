---
title: 유니코드 데이터 및 서버 코드 페이지 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- metadata [SQL Server], stored procedures
- Unicode [SQL Server], extended stored procedures
- extended stored procedures [SQL Server], metadata
ms.assetid: 52310260-a892-4b27-ad2e-bf164b98ee80
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cbf78cf6c3ed1b04dd0a282c016db83837bf0a0f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62742129"
---
# <a name="unicode-data-and-server-code-pages"></a>유니코드 데이터 및 서버 코드 페이지
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하십시오.  
  
 확장 저장 프로시저 API는 유니코드 데이터에 사용되지만 유니코드 메타데이터에는 사용되지 않습니다. #define 유니코드 지시문은 확장 저장 프로시저 API에 적용되지 않습니다.  
  
 확장 저장 프로시저 응용 프로그램에 의해 반환되거나 확장 저장 프로시저 API에 제공되는 모든 메타데이터는 서버의 멀티바이트 코드 페이지에 있는 것으로 가정됩니다. 확장 저장 프로시저 API 서버 응용 프로그램의 기본 코드 페이지는 호출 하 여 가져올 수 있는 응용 프로그램이 실행 되는 컴퓨터의 ANSI 코드 페이지로 **srv_pfield** SRV_로 필드 매개 변수를 사용 하 여 SPROC_CODEPAGE 합니다.  
  
 확장 저장 프로시저 API 응용 프로그램에서 유니코드를 사용하는 경우 이 데이터를 확장 저장 프로시저 API로 전달하기 전에 유니코드 메타데이터 열 이름, 오류 메시지 등을 멀티바이트 데이터로 변환해야 합니다.  
  
## <a name="example"></a>예제  
 다음 확장 저장 프로시저는 설명된 유니코드 변환의 예를 제공합니다. 다음 사항에 유의합니다.  
  
-   열 데이터는 유니코드 데이터로 전달 됩니다 **srv_describe** 열이 srvnvarchar 설명 되어 있으므로.  
  
-   열 이름 메타 데이터는 전달할 **srv_describe** 멀티 바이트 데이터로 합니다.  
  
     확장 저장 프로시저 호출 **srv_pfield** 필드 매개 변수를 SRV_SPROC_CODEPAGE로 설정의 멀티 바이트 코드 페이지를 가져오려고 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
-   오류 메시지를 전달할 **srv_sendmsg** 멀티 바이트 데이터로 합니다.  
  
    ```  
    __declspec(dllexport) RETCODE proc1 (SRV_PROC *srvproc)  
    {  
        #define MAX_COL_NAME_LEN 25  
        #define MAX_COL_DATA_LEN 50  
        #define MAX_ERR_MSG_LEN 250  
        #define MAX_SERVER_ERROR 20000  
        #define XP_ERROR_NUMBER MAX_SERVER_ERROR+1  
  
        int retval;  
        UINT serverCodePage;  
        CHAR *szServerCodePage;  
  
        WCHAR unicodeColumnName[MAX_COL_NAME_LEN];  
        CHAR multibyteColumnName[MAX_COL_NAME_LEN];  
  
        WCHAR unicodeColumnData[MAX_COL_DATA_LEN];  
  
        WCHAR unicodeErrorMessage[MAX_ERR_MSG_LEN];  
        CHAR  multibyteErrorMessage[MAX_ERR_MSG_LEN];  
  
        lstrcpyW (unicodeColumnName, L"column1");  
        lstrcpyW (unicodeColumnData, L"column1 data");  
        lstrcpyW (unicodeErrorMessage, L"No Error!");  
  
        // Obtain server code page.  
        //  
        szServerCodePage = srv_pfield (srvproc, SRV_SPROC_CODEPAGE, NULL);      
        if (NULL != szServerCodePage)  
            serverCodePage = atol(szServerCodePage);  
        else   
        {   // Problem situation exists.  
            srv_senddone(srvproc, (SRV_DONE_ERROR | SRV_DONE_MORE), 0, 0);  
            return 1;  
        }  
  
        // Convert column name for Unicode to multibyte using the   
        // server code page.  
        //  
        retval = WideCharToMultiByte(    
            serverCodePage,                 // code page  
            0,                              // default  
            unicodeColumnName,              // wide-character string  
            -1,                             // string is null terminated  
            multibyteColumnName,            // address of buffer for new  
                                            //   string  
            sizeof (multibyteColumnName),   // size of buffer  
            NULL, NULL);  
  
        if (0 == retval)  
        {  
            lstrcpyW (unicodeErrorMessage, L"Conversion to multibyte  
            failed.");  
            goto Error;  
        }  
  
        retval = srv_describe (srvproc, 1, multibyteColumnName,  
        SRV_NULLTERM,   
          SRVNVARCHAR, MAX_COL_DATA_LEN*sizeof(WCHAR), // destination  
            SRVNVARCHAR, lstrlenW(unicodeColumnData)*sizeof(WCHAR),  
            unicodeColumnData); //source  
        if (FAIL == retval)  
        {  
            lstrcpyW (unicodeErrorMessage, L"srv_describe failed.");  
            goto Error;  
        }  
  
       retval = srv_sendrow(srvproc);  
        if (FAIL == retval)  
        {  
            lstrcpyW (unicodeErrorMessage, L"srv_sendrow failed.");  
            goto Error;  
        }  
  
        retval = srv_senddone (srvproc, SRV_DONE_MORE|SRV_DONE_COUNT, 0, 1);  
        if (FAIL == retval)  
        {  
            lstrcpyW (unicodeErrorMessage, L"srv_senddone failed.");  
            goto Error;  
        }  
  
        return 0;  
    Error:  
        // convert error message from Unicode to multibyte.  
        retval = WideCharToMultiByte(    
            serverCodePage,                 // code page  
            0,                              // default  
            unicodeErrorMessage,            // wide-character string  
            -1,                             // string is null terminated  
            multibyteErrorMessage,          // address of buffer for new  
                                            //   string  
            sizeof (multibyteErrorMessage), // size of buffer  
            NULL, NULL);  
  
    srv_sendmsg(srvproc, SRV_MSG_ERROR, XP_ERROR_NUMBER, SRV_INFO, 1,  
                NULL, 0, __LINE__,   
                multibyteErrorMessage,  
                SRV_NULLTERM);  
  
        srv_senddone(srvproc, (SRV_DONE_ERROR | SRV_DONE_MORE), 0, 0);  
  
        return 1;  
    }  
  
    ```  
  
## <a name="see-also"></a>관련 항목  
 [srv_wsendmsg &#40;확장 저장 프로시저 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-wsendmsg-extended-stored-procedure-api.md)  
  
  
