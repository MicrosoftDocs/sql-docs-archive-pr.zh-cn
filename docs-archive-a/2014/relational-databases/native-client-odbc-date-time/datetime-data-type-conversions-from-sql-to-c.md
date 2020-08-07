---
title: 从 SQL 到 C 的转换 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC], SQL to C
ms.assetid: 059431e2-a65c-4587-ba4a-9929a1611e96
author: rothja
ms.author: jroth
ms.openlocfilehash: 0cc1fe6049824217a12a291b7006599a4a3a7319
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589029"
---
# <a name="conversions-from-sql-to-c"></a><span data-ttu-id="03b11-102">由 SQL 转换为 C</span><span class="sxs-lookup"><span data-stu-id="03b11-102">Conversions from SQL to C</span></span>
  <span data-ttu-id="03b11-103">下表列出了从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期/时间类型转换为 C 类型时要注意的问题。</span><span class="sxs-lookup"><span data-stu-id="03b11-103">The following table lists issues to consider when you convert from [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] date/time types to C types.</span></span>  
  
## <a name="conversions"></a><span data-ttu-id="03b11-104">转换</span><span class="sxs-lookup"><span data-stu-id="03b11-104">Conversions</span></span>  
  
||||||||||  
|-|-|-|-|-|-|-|-|-|  
||<span data-ttu-id="03b11-105">SQL_C_DATE</span><span class="sxs-lookup"><span data-stu-id="03b11-105">SQL_C_DATE</span></span>|<span data-ttu-id="03b11-106">SQL_C_TIME</span><span class="sxs-lookup"><span data-stu-id="03b11-106">SQL_C_TIME</span></span>|<span data-ttu-id="03b11-107">SQL_C_TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="03b11-107">SQL_C_TIMESTAMP</span></span>|<span data-ttu-id="03b11-108">SQL_C_SS_TIME2</span><span class="sxs-lookup"><span data-stu-id="03b11-108">SQL_C_SS_TIME2</span></span>|<span data-ttu-id="03b11-109">SQL_C_SS_TIMESTAMPOFFSET</span><span class="sxs-lookup"><span data-stu-id="03b11-109">SQL_C_SS_TIMESTAMPOFFSET</span></span>|<span data-ttu-id="03b11-110">SQL_C_BINARY</span><span class="sxs-lookup"><span data-stu-id="03b11-110">SQL_C_BINARY</span></span>|<span data-ttu-id="03b11-111">SQL_C_CHAR</span><span class="sxs-lookup"><span data-stu-id="03b11-111">SQL_C_CHAR</span></span>|<span data-ttu-id="03b11-112">SQL_C_WCHAR</span><span class="sxs-lookup"><span data-stu-id="03b11-112">SQL_C_WCHAR</span></span>|  
|<span data-ttu-id="03b11-113">SQL_CHAR</span><span class="sxs-lookup"><span data-stu-id="03b11-113">SQL_CHAR</span></span>|<span data-ttu-id="03b11-114">2、3、4、5</span><span class="sxs-lookup"><span data-stu-id="03b11-114">2,3,4,5</span></span>|<span data-ttu-id="03b11-115">2、3、6、7、8</span><span class="sxs-lookup"><span data-stu-id="03b11-115">2,3,6,7,8</span></span>|<span data-ttu-id="03b11-116">2、3、9、10、11</span><span class="sxs-lookup"><span data-stu-id="03b11-116">2,3,9,10,11</span></span>|<span data-ttu-id="03b11-117">2、3、6、7</span><span class="sxs-lookup"><span data-stu-id="03b11-117">2,3,6,7</span></span>|<span data-ttu-id="03b11-118">2、3、9、10、11</span><span class="sxs-lookup"><span data-stu-id="03b11-118">2,3,9,10,11</span></span>|<span data-ttu-id="03b11-119">1</span><span class="sxs-lookup"><span data-stu-id="03b11-119">1</span></span>|<span data-ttu-id="03b11-120">1</span><span class="sxs-lookup"><span data-stu-id="03b11-120">1</span></span>|<span data-ttu-id="03b11-121">1</span><span class="sxs-lookup"><span data-stu-id="03b11-121">1</span></span>|  
|<span data-ttu-id="03b11-122">SQL_WCHAR</span><span class="sxs-lookup"><span data-stu-id="03b11-122">SQL_WCHAR</span></span>|<span data-ttu-id="03b11-123">2、3、4、5</span><span class="sxs-lookup"><span data-stu-id="03b11-123">2,3,4,5</span></span>|<span data-ttu-id="03b11-124">2、3、6、7、8</span><span class="sxs-lookup"><span data-stu-id="03b11-124">2,3,6,7,8</span></span>|<span data-ttu-id="03b11-125">2、3、9、10、11</span><span class="sxs-lookup"><span data-stu-id="03b11-125">2,3,9,10,11</span></span>|<span data-ttu-id="03b11-126">2、3、6、7</span><span class="sxs-lookup"><span data-stu-id="03b11-126">2,3,6,7</span></span>|<span data-ttu-id="03b11-127">2、3、9、10、11</span><span class="sxs-lookup"><span data-stu-id="03b11-127">2,3,9,10,11</span></span>|<span data-ttu-id="03b11-128">1</span><span class="sxs-lookup"><span data-stu-id="03b11-128">1</span></span>|<span data-ttu-id="03b11-129">1</span><span class="sxs-lookup"><span data-stu-id="03b11-129">1</span></span>|<span data-ttu-id="03b11-130">1</span><span class="sxs-lookup"><span data-stu-id="03b11-130">1</span></span>|  
|<span data-ttu-id="03b11-131">SQL_TYPE_DATE</span><span class="sxs-lookup"><span data-stu-id="03b11-131">SQL_TYPE_DATE</span></span>|<span data-ttu-id="03b11-132">确定</span><span class="sxs-lookup"><span data-stu-id="03b11-132">OK</span></span>|<span data-ttu-id="03b11-133">12</span><span class="sxs-lookup"><span data-stu-id="03b11-133">12</span></span>|<span data-ttu-id="03b11-134">13</span><span class="sxs-lookup"><span data-stu-id="03b11-134">13</span></span>|<span data-ttu-id="03b11-135">12</span><span class="sxs-lookup"><span data-stu-id="03b11-135">12</span></span>|<span data-ttu-id="03b11-136">13、23</span><span class="sxs-lookup"><span data-stu-id="03b11-136">13,23</span></span>|<span data-ttu-id="03b11-137">14</span><span class="sxs-lookup"><span data-stu-id="03b11-137">14</span></span>|<span data-ttu-id="03b11-138">16</span><span class="sxs-lookup"><span data-stu-id="03b11-138">16</span></span>|<span data-ttu-id="03b11-139">16</span><span class="sxs-lookup"><span data-stu-id="03b11-139">16</span></span>|  
|<span data-ttu-id="03b11-140">SQL_SS_TIME2</span><span class="sxs-lookup"><span data-stu-id="03b11-140">SQL_SS_TIME2</span></span>|<span data-ttu-id="03b11-141">12</span><span class="sxs-lookup"><span data-stu-id="03b11-141">12</span></span>|<span data-ttu-id="03b11-142">8</span><span class="sxs-lookup"><span data-stu-id="03b11-142">8</span></span>|<span data-ttu-id="03b11-143">15</span><span class="sxs-lookup"><span data-stu-id="03b11-143">15</span></span>|<span data-ttu-id="03b11-144">确定</span><span class="sxs-lookup"><span data-stu-id="03b11-144">OK</span></span>|<span data-ttu-id="03b11-145">10，23</span><span class="sxs-lookup"><span data-stu-id="03b11-145">10,23</span></span>|<span data-ttu-id="03b11-146">17</span><span class="sxs-lookup"><span data-stu-id="03b11-146">17</span></span>|<span data-ttu-id="03b11-147">16</span><span class="sxs-lookup"><span data-stu-id="03b11-147">16</span></span>|<span data-ttu-id="03b11-148">16</span><span class="sxs-lookup"><span data-stu-id="03b11-148">16</span></span>|  
|<span data-ttu-id="03b11-149">SQL_TYPE_TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="03b11-149">SQL_TYPE_TIMESTAMP</span></span>|<span data-ttu-id="03b11-150">18</span><span class="sxs-lookup"><span data-stu-id="03b11-150">18</span></span>|<span data-ttu-id="03b11-151">7、8</span><span class="sxs-lookup"><span data-stu-id="03b11-151">7,8</span></span>|<span data-ttu-id="03b11-152">确定</span><span class="sxs-lookup"><span data-stu-id="03b11-152">OK</span></span>|<span data-ttu-id="03b11-153">7</span><span class="sxs-lookup"><span data-stu-id="03b11-153">7</span></span>|<span data-ttu-id="03b11-154">23</span><span class="sxs-lookup"><span data-stu-id="03b11-154">23</span></span>|<span data-ttu-id="03b11-155">19</span><span class="sxs-lookup"><span data-stu-id="03b11-155">19</span></span>|<span data-ttu-id="03b11-156">16</span><span class="sxs-lookup"><span data-stu-id="03b11-156">16</span></span>|<span data-ttu-id="03b11-157">16</span><span class="sxs-lookup"><span data-stu-id="03b11-157">16</span></span>|  
|<span data-ttu-id="03b11-158">SQL_SS_TIMESTAMPOFFSET</span><span class="sxs-lookup"><span data-stu-id="03b11-158">SQL_SS_TIMESTAMPOFFSET</span></span>|<span data-ttu-id="03b11-159">18、22</span><span class="sxs-lookup"><span data-stu-id="03b11-159">18,22</span></span>|<span data-ttu-id="03b11-160">7、8、20</span><span class="sxs-lookup"><span data-stu-id="03b11-160">7,8,20</span></span>|<span data-ttu-id="03b11-161">20</span><span class="sxs-lookup"><span data-stu-id="03b11-161">20</span></span>|<span data-ttu-id="03b11-162">7、20</span><span class="sxs-lookup"><span data-stu-id="03b11-162">7,20</span></span>|<span data-ttu-id="03b11-163">确定</span><span class="sxs-lookup"><span data-stu-id="03b11-163">OK</span></span>|<span data-ttu-id="03b11-164">21</span><span class="sxs-lookup"><span data-stu-id="03b11-164">21</span></span>|<span data-ttu-id="03b11-165">16</span><span class="sxs-lookup"><span data-stu-id="03b11-165">16</span></span>|<span data-ttu-id="03b11-166">16</span><span class="sxs-lookup"><span data-stu-id="03b11-166">16</span></span>|  
  
## <a name="key-to-symbols"></a><span data-ttu-id="03b11-167">符号含义</span><span class="sxs-lookup"><span data-stu-id="03b11-167">Key to Symbols</span></span>  
  
|<span data-ttu-id="03b11-168">符号</span><span class="sxs-lookup"><span data-stu-id="03b11-168">Symbol</span></span>|<span data-ttu-id="03b11-169">含义</span><span class="sxs-lookup"><span data-stu-id="03b11-169">Meaning</span></span>|  
|------------|-------------|  
|<span data-ttu-id="03b11-170">确定</span><span class="sxs-lookup"><span data-stu-id="03b11-170">OK</span></span>|<span data-ttu-id="03b11-171">无转换问题。</span><span class="sxs-lookup"><span data-stu-id="03b11-171">No conversion issues.</span></span>|  
|<span data-ttu-id="03b11-172">1</span><span class="sxs-lookup"><span data-stu-id="03b11-172">1</span></span>|<span data-ttu-id="03b11-173">应用 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 之前的规则。</span><span class="sxs-lookup"><span data-stu-id="03b11-173">Rules prior to [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] apply.</span></span>|  
|<span data-ttu-id="03b11-174">2</span><span class="sxs-lookup"><span data-stu-id="03b11-174">2</span></span>|<span data-ttu-id="03b11-175">忽略前导空格和尾随空格。</span><span class="sxs-lookup"><span data-stu-id="03b11-175">Leading and trailing spaces are ignored.</span></span>|  
|<span data-ttu-id="03b11-176">3</span><span class="sxs-lookup"><span data-stu-id="03b11-176">3</span></span>|<span data-ttu-id="03b11-177">字符串解析为日期、时间、时区或时区偏移量，且秒的小数部分允许多达 9 位。</span><span class="sxs-lookup"><span data-stu-id="03b11-177">The string is parsed into a date, time, timezone, or timezoneoffset, and allows up to 9 digits for fractional seconds.</span></span> <span data-ttu-id="03b11-178">如果解析时区偏移量，则时间将转换为客户端时区。</span><span class="sxs-lookup"><span data-stu-id="03b11-178">If a timezoneoffset is parsed, the time is converted to the client timezone.</span></span> <span data-ttu-id="03b11-179">如果在此转换过程中出现错误，将生成包含 SQLSTATE 22018 和消息 "日期时间字段溢出" 的诊断记录。</span><span class="sxs-lookup"><span data-stu-id="03b11-179">If an error occurs during this conversion, a diagnostic record is generated with SQLSTATE 22018 and the message "Datetime field overflow".</span></span>|  
|<span data-ttu-id="03b11-180">4</span><span class="sxs-lookup"><span data-stu-id="03b11-180">4</span></span>|<span data-ttu-id="03b11-181">如果该值不是有效的日期、时间戳或时间戳偏移量值，则生成具有 SQLSTATE 22018 和消息“为转换指定的字符值无效”的诊断记录。</span><span class="sxs-lookup"><span data-stu-id="03b11-181">If the value is not a valid date, timestamp, or timestampoffset value, a diagnostic record is generated with SQLSTATE 22018 and the message "Invalid character value for cast specification".</span></span>|  
|<span data-ttu-id="03b11-182">5</span><span class="sxs-lookup"><span data-stu-id="03b11-182">5</span></span>|<span data-ttu-id="03b11-183">如果时间为非零，则生成具有 SQLSTATE 01S07 和消息“截断小数部分”的诊断记录。</span><span class="sxs-lookup"><span data-stu-id="03b11-183">If the time is non-zero, a diagnostic record is generated with SQLSTATE 01S07 and the message "Fractional truncation".</span></span>|  
|<span data-ttu-id="03b11-184">6</span><span class="sxs-lookup"><span data-stu-id="03b11-184">6</span></span>|<span data-ttu-id="03b11-185">如果该值不是有效的时间、时间戳或时间戳偏移量值，则生成具有 SQLSTATE 22018 和消息“为转换指定的字符值无效”的诊断记录。</span><span class="sxs-lookup"><span data-stu-id="03b11-185">If the value is not a valid time, timestamp, or timestampoffset value, a diagnostic record is generated with SQLSTATE 22018 and the message "Invalid character value for cast specification".</span></span>|  
|<span data-ttu-id="03b11-186">7</span><span class="sxs-lookup"><span data-stu-id="03b11-186">7</span></span>|<span data-ttu-id="03b11-187">忽略日期部分。</span><span class="sxs-lookup"><span data-stu-id="03b11-187">The date component is ignored.</span></span>|  
|<span data-ttu-id="03b11-188">8</span><span class="sxs-lookup"><span data-stu-id="03b11-188">8</span></span>|<span data-ttu-id="03b11-189">如果秒的小数部分为非零，则生成具有 SQLSTATE 01S07 和消息“截断小数部分”的诊断记录。</span><span class="sxs-lookup"><span data-stu-id="03b11-189">If the fractional seconds are non-zero, a diagnostic record is generated with SQLSTATE 01S07 and the message "Fractional truncation".</span></span>|  
|<span data-ttu-id="03b11-190">9</span><span class="sxs-lookup"><span data-stu-id="03b11-190">9</span></span>|<span data-ttu-id="03b11-191">如果该值不是有效的日期、时间、时间戳或 timestampoffset 值，则会生成包含 SQLSTATE 22018 的诊断记录和消息 "对于 cast 规范无效的字符值"。</span><span class="sxs-lookup"><span data-stu-id="03b11-191">If the value is not a valid date, time, timestamp, or timestampoffset value, a diagnostic record is generated with SQLSTATE 22018 and the message "Invalid character value for cast specification".</span></span>|  
|<span data-ttu-id="03b11-192">10</span><span class="sxs-lookup"><span data-stu-id="03b11-192">10</span></span>|<span data-ttu-id="03b11-193">如果该值是有效的时间，则日期部分设置为当前客户端的日期。</span><span class="sxs-lookup"><span data-stu-id="03b11-193">If the value is a valid time, the date component is set to current client date.</span></span>|  
|<span data-ttu-id="03b11-194">11</span><span class="sxs-lookup"><span data-stu-id="03b11-194">11</span></span>|<span data-ttu-id="03b11-195">如果该值是有效的日期，则时间设置为零。</span><span class="sxs-lookup"><span data-stu-id="03b11-195">If the value is a valid date, the time is set to zero.</span></span>|  
|<span data-ttu-id="03b11-196">12</span><span class="sxs-lookup"><span data-stu-id="03b11-196">12</span></span>|<span data-ttu-id="03b11-197">生成具有 SQLSTATE 07006 和消息“受限制的数据类型属性冲突”的诊断记录。</span><span class="sxs-lookup"><span data-stu-id="03b11-197">A diagnostic record is generated with SQLSTATE 07006 and the message "Restricted data type attribute violation".</span></span>|  
|<span data-ttu-id="03b11-198">13</span><span class="sxs-lookup"><span data-stu-id="03b11-198">13</span></span>|<span data-ttu-id="03b11-199">时间设置为零。</span><span class="sxs-lookup"><span data-stu-id="03b11-199">The time is set to zero.</span></span>|  
|<span data-ttu-id="03b11-200">14</span><span class="sxs-lookup"><span data-stu-id="03b11-200">14</span></span>|<span data-ttu-id="03b11-201">如果缓冲区不足以容纳 SQL_DATE_STRUCT，则生成具有 SQLSTATE 22003 和消息“数值超出了范围”的诊断记录。</span><span class="sxs-lookup"><span data-stu-id="03b11-201">If the buffer is not large enough to accommodate a SQL_DATE_STRUCT, a diagnostic record is generated with SQLSTATE 22003 and the message "Numeric value out of range".</span></span>|  
|<span data-ttu-id="03b11-202">15</span><span class="sxs-lookup"><span data-stu-id="03b11-202">15</span></span>|<span data-ttu-id="03b11-203">日期设置为当前客户端的日期。</span><span class="sxs-lookup"><span data-stu-id="03b11-203">The date is set to the current client date.</span></span>|  
|<span data-ttu-id="03b11-204">16</span><span class="sxs-lookup"><span data-stu-id="03b11-204">16</span></span>|<span data-ttu-id="03b11-205">如果缓冲区不足以容纳转换后的字符串值，只能容纳秒的小数部分，则会发生截断，且生成具有 SQLSTATE 01004 和消息“字符串数据，右端被截断”的诊断记录。</span><span class="sxs-lookup"><span data-stu-id="03b11-205">If the buffer is not large enough to accommodate the converted string value but only fractional seconds, truncation occurs and a diagnostic record is generated with SQLSTATE 01004 and the message "String data, right truncated".</span></span> <span data-ttu-id="03b11-206">如果缓冲区不足以容纳未截断日期、时间或偏移量部分的字符串值，则生成具有 SQLSTATE 22003 和消息“数值超出了范围”的诊断记录。</span><span class="sxs-lookup"><span data-stu-id="03b11-206">If the buffer is not large enough to accommodate the string value without truncation of date, time, or offset components, a diagnostic record is generated with SQLSTATE 22003 and the message "Numeric value out of range".</span></span> <span data-ttu-id="03b11-207">请注意，对于日期和时间戳偏移量，由于转换后的字符串最右侧部分不包含秒的小数部分，因此不可能为 SQLSTATE 01004。</span><span class="sxs-lookup"><span data-stu-id="03b11-207">Note that for date and timestampoffset, SQLSTATE 01004 is not possible because the rightmost part of the converted string does not contain fractional seconds.</span></span> <span data-ttu-id="03b11-208">因此，任何截断都会造成数据丢失。</span><span class="sxs-lookup"><span data-stu-id="03b11-208">Therefore, any truncation causes data loss.</span></span>|  
|<span data-ttu-id="03b11-209">17</span><span class="sxs-lookup"><span data-stu-id="03b11-209">17</span></span>|<span data-ttu-id="03b11-210">如果缓冲区不足以容纳 SQL_SS_TIME2_STRUCT，则生成具有 SQLSTATE 22003 和消息“数值超出了范围”的诊断记录。</span><span class="sxs-lookup"><span data-stu-id="03b11-210">If the buffer is not large enough to accommodate a SQL_SS_TIME2_STRUCT, a diagnostic record is generated with SQLSTATE 22003 and the message "Numeric value out of range".</span></span>|  
|<span data-ttu-id="03b11-211">18</span><span class="sxs-lookup"><span data-stu-id="03b11-211">18</span></span>|<span data-ttu-id="03b11-212">如果时间为非零，则生成具有 SQLSTATE 01S07 和消息“截断小数部分”的诊断记录。</span><span class="sxs-lookup"><span data-stu-id="03b11-212">If the time is non-zero, a diagnostic record is generated with SQLSTATE 01S07 and the message "Fractional truncation".</span></span>|  
|<span data-ttu-id="03b11-213">19</span><span class="sxs-lookup"><span data-stu-id="03b11-213">19</span></span>|<span data-ttu-id="03b11-214">如果服务器类型为 datetime 或 smalldatetime，则值对应于 TDS 连网格式，对于 smalldatetime 为 4 字节值，对于 datetime 为 8 字节值。</span><span class="sxs-lookup"><span data-stu-id="03b11-214">If the server type is datetime or smalldatetime, the value corresponds to the TDS wire format and will be a 4-byte value for smalldatetime and an 8-byte value for datetime.</span></span><br /><br /> <span data-ttu-id="03b11-215">如果服务器类型为 datetime2，则按照 SQL_TIMESTAMP_STRUCT 返回值。</span><span class="sxs-lookup"><span data-stu-id="03b11-215">If the server type is datetime2, the value is returned as a SQL_TIMESTAMP_STRUCT.</span></span> <span data-ttu-id="03b11-216">如果缓冲区不足以容纳返回值，则生成具有 SQLSTATE 22003 和消息“数值超出了范围”的诊断记录。</span><span class="sxs-lookup"><span data-stu-id="03b11-216">If the buffer is not large enough to accommodate the returned value, a diagnostic record is generated with SQLSTATE 22003 and the message "Numeric value out of range".</span></span>|  
|<span data-ttu-id="03b11-217">20</span><span class="sxs-lookup"><span data-stu-id="03b11-217">20</span></span>|<span data-ttu-id="03b11-218">将时间转换为客户端时区。</span><span class="sxs-lookup"><span data-stu-id="03b11-218">The time is converted to the client timezone.</span></span> <span data-ttu-id="03b11-219">如果在此转换过程中发生错误，则生成具有 SQLSTATE 22008 和消息“日期时间字段溢出”的诊断记录。</span><span class="sxs-lookup"><span data-stu-id="03b11-219">If an error occurs during this conversion, a diagnostic record is generated with SQLSTATE 22008 and the message "Datetime field overflow".</span></span>|  
|<span data-ttu-id="03b11-220">21</span><span class="sxs-lookup"><span data-stu-id="03b11-220">21</span></span>|<span data-ttu-id="03b11-221">如果缓冲区足以容纳 SQL_SS_TIMESTAMPOFFSET_STRUCT，则按照 SQL_SS_TIMESTAMPOFFSET_STRUCT 返回值。</span><span class="sxs-lookup"><span data-stu-id="03b11-221">If the buffer is large enough to accommodate a SQL_SS_TIMESTAMPOFFSET_STRUCT, the value is returned as a SQL_SS_TIMESTAMPOFFSET_STRUCT.</span></span> <span data-ttu-id="03b11-222">否则，生成具有 SQLSTATE 22003 和消息“数值超出了范围”的诊断记录。</span><span class="sxs-lookup"><span data-stu-id="03b11-222">Otherwise, a diagnostic record is generated with SQLSTATE 22003 and the message "Numeric value out of range".</span></span>|  
|<span data-ttu-id="03b11-223">22</span><span class="sxs-lookup"><span data-stu-id="03b11-223">22</span></span>|<span data-ttu-id="03b11-224">在提取日期之前，将值转换为客户端时区。</span><span class="sxs-lookup"><span data-stu-id="03b11-224">The value is converted to the client timezone before the date is extracted.</span></span> <span data-ttu-id="03b11-225">这提供了与其他时间戳偏移量类型转换的一致性。</span><span class="sxs-lookup"><span data-stu-id="03b11-225">This provides consistency with other conversions with timestampoffset types.</span></span> <span data-ttu-id="03b11-226">如果在此转换过程中发生错误，则生成具有 SQLSTATE 22008 和消息“日期时间字段溢出”的诊断记录。</span><span class="sxs-lookup"><span data-stu-id="03b11-226">If an error occurs during this conversion, a diagnostic record is generated with SQLSTATE 22008 and the message "Datetime field overflow".</span></span> <span data-ttu-id="03b11-227">这可能会导致日期与通过简单截断获得的值不同。</span><span class="sxs-lookup"><span data-stu-id="03b11-227">This might result in a date that differs from the value obtained by simple truncation.</span></span>|  
  
 <span data-ttu-id="03b11-228">本主题中的表格列出了返回客户端的类型与绑定中的类型之间的转换。</span><span class="sxs-lookup"><span data-stu-id="03b11-228">The table in this topic describes conversions between the type returned to the client and the type in the binding.</span></span> <span data-ttu-id="03b11-229">对于输出参数，如果 SQLBindParameter 中指定的服务器类型与服务器上的实际类型不匹配，则服务器将执行隐式转换，并且返回给客户端的类型将与通过 SQLBindParameter 指定的类型匹配。</span><span class="sxs-lookup"><span data-stu-id="03b11-229">For output parameters, if the server type specified in SQLBindParameter does not match the actual type on the server, an implicit conversion will be performed by the server and the type returned to the client will match the type specified through SQLBindParameter.</span></span> <span data-ttu-id="03b11-230">当服务器的转换规则与上表中列出的规则不同时，这可能会导致意外的转换结果。</span><span class="sxs-lookup"><span data-stu-id="03b11-230">This can lead to unexpected conversion results when the server's conversion rules are different from those listed in the preceding table.</span></span> <span data-ttu-id="03b11-231">例如，在必须提供默认日期时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 1900-1-1，而不是当前日期。</span><span class="sxs-lookup"><span data-stu-id="03b11-231">For example, when a default date must be provided, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] uses 1900-1-1, rather than the current date.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="03b11-232">另请参阅</span><span class="sxs-lookup"><span data-stu-id="03b11-232">See Also</span></span>  
 [<span data-ttu-id="03b11-233">ODBC&#41;&#40;的日期和时间改进</span><span class="sxs-lookup"><span data-stu-id="03b11-233">Date and Time Improvements &#40;ODBC&#41;</span></span>](date-and-time-improvements-odbc.md)  
  
  