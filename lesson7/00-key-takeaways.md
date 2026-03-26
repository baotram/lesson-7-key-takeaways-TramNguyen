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












