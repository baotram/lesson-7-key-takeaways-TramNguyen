1. DOM
    * DOM relation
        . self: node hiện tại 
        . parent: cha - node phía trên trực tiếp của node hiện tại
        . children: con - node phía dưới trực tiếp của node hiện tại 
        . ancestor: tổ tiên - các node cha, cha của cha, ...
        . descendant: hậu duệ - các node con, cháu chắt
        . sibling: anh em - phần tử cùng cấp và cùng cha
        . following: các node sau của node hiện tại (không gồm thằng con của node hiện tại)
        . preceding: các node trên trừ các node ancestor của node hiện tại
        . following-sibling: node anh em phía sau của node hiện tại
        . preceding-sibling: node anh em phía trước của node hiện tại 


2. XPath axes 
    * Là phương pháp để điều hướng và chọn các node trên cây DOM XML/HTML dựa trên mối quan hệ giữa các node với nhau
    - Tìm kiếm elements dựa trên vị trí tương đối (parent, child, sibling, ancestor...)
    - Linh hoạt hơn việc chỉ dùng đường dẫn tuyệt đối hoặc tương đối
    * Wildcard: *
    - Nghĩa là khớp tất cả
VD:
//div -> khớp thẻ div
//* -> khớp tất cả các loại thẻ
    * child - Con trực tiếp
VD:  Tìm tất cả các button con trực tiếp của form
      //form[@id='test-form']/child::button
    * descendant - Tất cả con cháu
VD: Tìm tất cả input bên trong form (mọi cấp)
//form[@id='test-form']/descendant::input
    * parent - Tìm cha
VD: Tìm form cha của button "Create Test Case" 
//button[text()='Create Test Case']/parent::form
    * ancestor - Tìm tổ tiên
VD: Từ button "Edit" trong table, tìm table tổ tiên 
//button[@class='btn-edit']/ancestor::table
    * following-sibling - Anh em phía sau
VD: Từ label "Test Case Name", tìm input cùng cấp ngay sau nó
//label[@for='testName']/following-sibling::input
    * preceding-sibling - Anh em đứng trước
VD: Từ button "Reset Form", tìm button đứng trước nó
//button[@class='btn-reset']/preceding-sibling::button
    * following - Tất cả node sau trong document
    * ancestor-or-self - Tổ tiên hoặc chính nó
    * preceding - Tất cả node trước trong document
    * descendant-or-self - Con cháu hoặc chính nó

==========>>>>>>> //tag/relationship::tagname[@attr=’value’] 

    * Chứa thuộc tính: @attribute
//tagname[@attribute='value']

    * AND và OR operators
AND - Tất cả điều kiện phải đúng
//element[@condition1 and @condition2]

OR - Một trong các điều kiện đúng
//element[@condition1 or @condition2]

Kết hợp AND và OR

    * Lấy text bên trong element
- text() lấy text node trực tiếp của element.
VD: //element[text()='exact text']
- normalize-space(): Chuẩn hóa khoảng trắng
Loại bỏ khoảng trắng thừa ở đầu, cuối và giữa text.
normalize-space(string)

    * contains(): Kiểm tra chứa chuỗi con
- //element[contains(@attribute, 'substring')]
- //element[contains(text(), 'substring')]

3. Assertion (khẳng định, xác nhận)
- câu lệnh để kiểm tra điều gì đó có đúng với mong đợi hay không (không có assertion = không biết test có thành công hay thất bại hay không)
- Playwright assert thông qua hàm expect
VD:
    import {test, expect} from 'playwright/test';
    test("Test 01", async({page})) => {
        <!-- Khẳng định rằng title trang phải là "Homepage" -->
        await expect(page).toHaveTitle("Homepage");
    }
- Các loại assertion: 
● Generic Assertions (từ thư viện expect): expect(giá trị) = (giá trị)
VD:
 expect(value).toBe(expected);
 expect(array).toHaveLength(3);
 expect(string).toContain('text');

● Web-first Assertions (auto-waiting): expect(phần tử) có giá trị
VD:
 await expect(page.locator('button')).toBeVisible();
 await expect(page).toHaveTitle(/Homepage/);
 
+ Element State
// Kiểm tra visibility
await expect(locator).toBeVisible();
await expect(locator).toBeHidden();
// Kiểm tra enabled/disabled
await expect(locator).toBeEnabled();
await expect(locator).toBeDisabled();
// Kiểm tra checked (checkbox/radio)
await expect(locator).toBeChecked();
// Kiểm tra focus
await expect(locator).toBeFocused();


+ Text & Content
// Có chứa text
await expect(locator).toContainText('Hello');
// Text chính xác
await expect(locator).toHaveText('Welcome');
// Text khớp regex
await expect(locator).toHaveText(/welcome/i);
// Kiểm tra nhiều elements
await expect(locator).toHaveText(['Item 1', 'Item 2']);

+ Attributes & Properties
// Kiểm tra attribute
await expect(locator).toHaveAttribute('href', '/about');
// Kiểm tra class
await expect(locator).toHaveClass('active');
await expect(locator).toHaveClass(/btn-primary/);
// Kiểm tra value (input fields)
await expect(locator).toHaveValue('john@example.com');
// Kiểm tra count
await expect(locator).toHaveCount(5);

+ Page Assertions
// URL
await expect(page).toHaveURL('https://example.com/');
await expect(page).toHaveURL(/.*checkout/);
// Title
await expect(page).toHaveTitle(/Playwright/);


*** Benefit of web-first assertion
- dùng web-first assertion: chờ flexible (trong tối đa 5s, nếu 1s đã xuất hiện thì thoát luôn)


