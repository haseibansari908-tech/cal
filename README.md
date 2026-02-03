<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>دفتر المصاريف اليومية</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
            direction: rtl;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }

        .header h1 {
            font-size: 28px;
            margin-bottom: 10px;
        }

        .header p {
            opacity: 0.9;
            font-size: 14px;
        }

        .form-section {
            padding: 30px;
            background: #f8f9fa;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            color: #333;
            font-weight: 600;
            font-size: 14px;
        }

        .form-group input,
        .form-group textarea,
        .form-group select {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            font-size: 16px;
            transition: all 0.3s;
            font-family: inherit;
        }

        .form-group input:focus,
        .form-group textarea:focus,
        .form-group select:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        .form-group textarea {
            resize: vertical;
            min-height: 80px;
        }

        .btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 10px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            width: 100%;
            transition: transform 0.2s;
        }

        .btn:active {
            transform: scale(0.98);
        }

        .expenses-section {
            padding: 30px;
        }

        .date-group {
            margin-bottom: 30px;
            border: 2px solid #e0e0e0;
            border-radius: 15px;
            overflow: hidden;
        }

        .date-header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 15px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .date-header h3 {
            font-size: 18px;
        }

        .date-total {
            font-size: 16px;
            font-weight: 600;
        }

        .expense-item {
            padding: 20px;
            border-bottom: 1px solid #e0e0e0;
            background: white;
            transition: background 0.2s;
        }

        .expense-item:hover {
            background: #f8f9fa;
        }

        .expense-item:last-child {
            border-bottom: none;
        }

        .expense-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }

        .expense-project {
            font-size: 18px;
            font-weight: 600;
            color: #333;
        }

        .expense-amount {
            font-size: 20px;
            font-weight: 700;
            color: #667eea;
        }

        .expense-notes {
            color: #666;
            font-size: 14px;
            line-height: 1.6;
            margin-top: 10px;
            padding: 10px;
            background: #f8f9fa;
            border-radius: 8px;
        }

        .expense-time {
            color: #999;
            font-size: 12px;
            margin-top: 5px;
        }

        .delete-btn {
            background: #dc3545;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 6px;
            font-size: 12px;
            cursor: pointer;
            margin-top: 10px;
        }

        .delete-btn:active {
            transform: scale(0.95);
        }

        .grand-total {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 25px 30px;
            text-align: center;
            font-size: 24px;
            font-weight: 700;
        }

        .grand-total-label {
            font-size: 16px;
            opacity: 0.9;
            margin-bottom: 10px;
        }

        .empty-state {
            text-align: center;
            padding: 60px 20px;
            color: #999;
        }

        .empty-state svg {
            width: 100px;
            height: 100px;
            margin-bottom: 20px;
            opacity: 0.3;
        }

        .currency {
            font-size: 0.9em;
            opacity: 0.9;
        }

        @media (max-width: 600px) {
            body {
                padding: 10px;
            }

            .header h1 {
                font-size: 24px;
            }

            .form-section,
            .expenses-section {
                padding: 20px;
            }

            .expense-header {
                flex-direction: column;
                align-items: flex-start;
                gap: 10px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>💰 دفتر المصاريف اليومية</h1>
            <p>سجل مصاريفك بسهولة وتابع ميزانيتك</p>
        </div>

        <div class="form-section">
            <form id="expenseForm">
                <div class="form-group">
                    <label>📅 التاريخ</label>
                    <input type="date" id="expenseDate" required>
                </div>

                <div class="form-group">
                    <label>📊 اسم المشروع أو البند</label>
                    <input type="text" id="projectName" placeholder="مثال: مشروع التسويق، مصاريف المكتب..." required>
                </div>

                <div class="form-group">
                    <label>💵 المبلغ (ريال)</label>
                    <input type="number" id="amount" step="0.01" placeholder="0.00" required>
                </div>

                <div class="form-group">
                    <label>📝 ملاحظات وتفاصيل</label>
                    <textarea id="notes" placeholder="أضف تفاصيل إضافية عن المصروف..."></textarea>
                </div>

                <button type="submit" class="btn">➕ إضافة مصروف</button>
            </form>
        </div>

        <div class="expenses-section">
            <div id="expensesList"></div>
        </div>

        <div class="grand-total">
            <div class="grand-total-label">إجمالي المصاريف</div>
            <div id="grandTotal">0.00 <span class="currency">ريال</span></div>
        </div>
    </div>

    <script>
        // تهيئة التطبيق
        class ExpenseTracker {
            constructor() {
                this.expenses = this.loadExpenses();
                this.initializeForm();
                this.render();
            }

            // تحميل البيانات من قاعدة البيانات المحلية
            loadExpenses() {
                const stored = localStorage.getItem('dailyExpenses');
                return stored ? JSON.parse(stored) : [];
            }

            // حفظ البيانات في قاعدة البيانات المحلية
            saveExpenses() {
                localStorage.setItem('dailyExpenses', JSON.stringify(this.expenses));
            }

            // تهيئة النموذج
            initializeForm() {
                const form = document.getElementById('expenseForm');
                const dateInput = document.getElementById('expenseDate');
                
                // تعيين التاريخ الحالي افتراضياً
                dateInput.valueAsDate = new Date();

                form.addEventListener('submit', (e) => {
                    e.preventDefault();
                    this.addExpense();
                });
            }

            // إضافة مصروف جديد
            addExpense() {
                const expense = {
                    id: Date.now(),
                    date: document.getElementById('expenseDate').value,
                    project: document.getElementById('projectName').value,
                    amount: parseFloat(document.getElementById('amount').value),
                    notes: document.getElementById('notes').value,
                    timestamp: new Date().toLocaleTimeString('ar-SA', { 
                        hour: '2-digit', 
                        minute: '2-digit' 
                    })
                };

                this.expenses.push(expense);
                this.saveExpenses();
                this.render();
                this.resetForm();
            }

            // حذف مصروف
            deleteExpense(id) {
                if (confirm('هل أنت متأكد من حذف هذا المصروف؟')) {
                    this.expenses = this.expenses.filter(exp => exp.id !== id);
                    this.saveExpenses();
                    this.render();
                }
            }

            // إعادة تعيين النموذج
            resetForm() {
                document.getElementById('projectName').value = '';
                document.getElementById('amount').value = '';
                document.getElementById('notes').value = '';
                document.getElementById('projectName').focus();
            }

            // تجميع المصاريف حسب التاريخ
            groupByDate() {
                const grouped = {};
                
                this.expenses.forEach(expense => {
                    if (!grouped[expense.date]) {
                        grouped[expense.date] = [];
                    }
                    grouped[expense.date].push(expense);
                });

                // ترتيب التواريخ من الأحدث للأقدم
                return Object.keys(grouped)
                    .sort((a, b) => new Date(b) - new Date(a))
                    .reduce((acc, date) => {
                        acc[date] = grouped[date];
                        return acc;
                    }, {});
            }

            // حساب إجمالي مصاريف يوم معين
            calculateDayTotal(expenses) {
                return expenses.reduce((sum, exp) => sum + exp.amount, 0);
            }

            // حساب الإجمالي الكلي
            calculateGrandTotal() {
                return this.expenses.reduce((sum, exp) => sum + exp.amount, 0);
            }

            // تنسيق التاريخ
            formatDate(dateString) {
                const date = new Date(dateString);
                const today = new Date();
                const yesterday = new Date(today);
                yesterday.setDate(yesterday.getDate() - 1);

                if (date.toDateString() === today.toDateString()) {
                    return 'اليوم';
                } else if (date.toDateString() === yesterday.toDateString()) {
                    return 'أمس';
                } else {
                    return date.toLocaleDateString('ar-SA', { 
                        weekday: 'long', 
                        year: 'numeric', 
                        month: 'long', 
                        day: 'numeric' 
                    });
                }
            }

            // تنسيق المبلغ
            formatAmount(amount) {
                return amount.toFixed(2).replace(/\B(?=(\d{3})+(?!\d))/g, ',');
            }

            // عرض البيانات
            render() {
                const expensesList = document.getElementById('expensesList');
                const grandTotalElement = document.getElementById('grandTotal');
                
                if (this.expenses.length === 0) {
                    expensesList.innerHTML = `
                        <div class="empty-state">
                            <svg viewBox="0 0 24 24" fill="currentColor">
                                <path d="M19 3h-4.18C14.4 1.84 13.3 1 12 1c-1.3 0-2.4.84-2.82 2H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zm-7 0c.55 0 1 .45 1 1s-.45 1-1 1-1-.45-1-1 .45-1 1-1zm0 4c1.66 0 3 1.34 3 3s-1.34 3-3 3-3-1.34-3-3 1.34-3 3-3zm6 12H6v-1.4c0-2 4-3.1 6-3.1s6 1.1 6 3.1V19z"/>
                            </svg>
                            <h3>لا توجد مصاريف مسجلة</h3>
                            <p>ابدأ بإضافة أول مصروف لك</p>
                        </div>
                    `;
                } else {
                    const groupedExpenses = this.groupByDate();
                    let html = '';

                    for (const [date, expenses] of Object.entries(groupedExpenses)) {
                        const dayTotal = this.calculateDayTotal(expenses);
                        
                        html += `
                            <div class="date-group">
                                <div class="date-header">
                                    <h3>${this.formatDate(date)}</h3>
                                    <div class="date-total">${this.formatAmount(dayTotal)} ريال</div>
                                </div>
                        `;

                        expenses.forEach(expense => {
                            html += `
                                <div class="expense-item">
                                    <div class="expense-header">
                                        <div class="expense-project">${expense.project}</div>
                                        <div class="expense-amount">${this.formatAmount(expense.amount)} ريال</div>
                                    </div>
                                    ${expense.notes ? `<div class="expense-notes">${expense.notes}</div>` : ''}
                                    <div class="expense-time">⏰ ${expense.timestamp}</div>
                                    <button class="delete-btn" onclick="tracker.deleteExpense(${expense.id})">🗑️ حذف</button>
                                </div>
                            `;
                        });

                        html += `</div>`;
                    }

                    expensesList.innerHTML = html;
                }

                // تحديث الإجمالي الكلي
                const grandTotal = this.calculateGrandTotal();
                grandTotalElement.innerHTML = `${this.formatAmount(grandTotal)} <span class="currency">ريال</span>`;
            }
        }

        // تشغيل التطبيق
        const tracker = new ExpenseTracker();
    </script>
</body>
</html>