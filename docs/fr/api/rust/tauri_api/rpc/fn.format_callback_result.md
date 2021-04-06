---
title: "fn.format_callback_result"
---

# Function [tauri_api](/docs/api/rust/tauri_api/../index.html)::​[rpc](/docs/api/rust/tauri_api/index.html)::​[format_callback_result](/docs/api/rust/tauri_api/)

    pub fn format_callback_result<T: Serialize, E: Serialize>(
        result: Result<T, E>, 
        success_callback: String, 
        error_callback: String
    ) -> Result<String>

Formats a Result type to its Promise response. Useful for Promises handling. If the Result `is_ok()`, the callback will be the `success_callback` function name and the argument will be the Ok value. If the Result `is_err()`, the callback will be the `error_callback` function name and the argument will be the Err value.

-   `result` the Result to check
-   `success_callback` the function name of the Ok callback. Usually the `resolve` of the JS Promise.
-   `error_callback` the function name of the Err callback. Usually the `reject` of the JS Promise.

# [Examples](/docs/api/rust/tauri_api/about:blank#examples)

    use tauri_api::rpc::format_callback_result;
    let res: Result<u8, &str> = Ok(5);
    let cb = format_callback_result(res, "success_cb".to_string(), "error_cb".to_string()).expect("failed to format");
    assert!(cb.contains(r#"window["success_cb"](5)"#));

    let res: Result<&str, &str> = Err("error message here");
    let cb = format_callback_result(res, "success_cb".to_string(), "error_cb".to_string()).expect("failed to format");
    assert!(cb.contains(r#"window["error_cb"]("error message here")"#));
