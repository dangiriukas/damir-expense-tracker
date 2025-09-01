# damir-expense-tracker

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Personal Finance & Meal Cost Tracker</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            padding: 30px;
        }
        
        .header {
            text-align: center;
            margin-bottom: 40px;
        }
        
        .header h1 {
            color: #2d3748;
            font-size: 2.5rem;
            margin-bottom: 10px;
            font-weight: 700;
        }
        
        .header p {
            color: #718096;
            font-size: 1.1rem;
        }
        
        .month-selector {
            background: white;
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 30px;
            text-align: center;
            box-shadow: 0 5px 15px rgba(0,0,0,0.08);
        }
        
        .month-selector select {
            padding: 12px 20px;
            border: 2px solid #e2e8f0;
            border-radius: 8px;
            font-size: 1.1rem;
            font-weight: 600;
            background: white;
            cursor: pointer;
            min-width: 200px;
        }
        
        .month-selector select:focus {
            outline: none;
            border-color: #667eea;
        }
        
        .month-label {
            margin-right: 15px;
            font-weight: 600;
            color: #2d3748;
            font-size: 1.1rem;
        }
        
        .tabs {
            display: flex;
            background: #f7fafc;
            border-radius: 15px;
            margin-bottom: 30px;
            overflow: hidden;
        }
        
        .tab {
            flex: 1;
            padding: 15px 20px;
            background: transparent;
            border: none;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s ease;
            color: #4a5568;
        }
        
        .tab.active {
            background: #667eea;
            color: white;
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        .form-section {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 30px;
        }
        
        .form-section h3 {
            color: #2d3748;
            margin-bottom: 20px;
            font-size: 1.4rem;
        }
        
        .form-row {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 15px;
        }
        
        .input-group {
            display: flex;
            flex-direction: column;
        }
        
        .input-group label {
            margin-bottom: 5px;
            font-weight: 600;
            color: #4a5568;
            font-size: 0.9rem;
        }
        
        .input-group input, .input-group select {
            padding: 12px;
            border: 2px solid #e2e8f0;
            border-radius: 8px;
            font-size: 1rem;
            transition: border-color 0.3s ease;
        }
        
        .input-group input:focus, .input-group select:focus {
            outline: none;
            border-color: #667eea;
        }
        
        .btn {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            transition: transform 0.2s ease;
        }
        
        .btn:hover {
            transform: translateY(-2px);
        }
        
        .btn-danger {
            background: #e53e3e;
        }
        
        .table-container {
            overflow-x: auto;
            background: white;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.08);
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
        }
        
        th, td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid #e2e8f0;
        }
        
        th {
            background: #f7fafc;
            font-weight: 600;
            color: #2d3748;
        }
        
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .stat-card {
            background: linear-gradient(135deg, #4c51bf, #667eea);
            color: white;
            padding: 25px;
            border-radius: 15px;
            text-align: center;
        }
        
        .stat-value {
            font-size: 2rem;
            font-weight: 700;
            margin-bottom: 5px;
        }
        
        .stat-label {
            font-size: 0.9rem;
            opacity: 0.9;
        }
        
        .ingredient-item {
            background: white;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 10px;
            border: 1px solid #e2e8f0;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .delete-btn {
            background: #e53e3e;
            color: white;
            border: none;
            padding: 6px 12px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 0.8rem;
        }
        
        .meal-cost {
            background: #48bb78;
            color: white;
            padding: 10px 20px;
            border-radius: 8px;
            font-weight: 600;
            font-size: 1.1rem;
            margin-top: 15px;
            text-align: center;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>💰 Finance Master</h1>
            <p>Track every cent, master every meal, control every expense</p>
        </div>
        
        <div class="month-selector">
            <span class="month-label">Viewing Month:</span>
            <select id="monthSelector" onchange="changeMonth()">
                <option value="2025-09">September 2025</option>
                <option value="2025-10">October 2025</option>
                <option value="2025-11">November 2025</option>
                <option value="2025-12">December 2025</option>
                <option value="2026-01">January 2026</option>
                <option value="2026-02">February 2026</option>
                <option value="2026-03">March 2026</option>
                <option value="2026-04">April 2026</option>
                <option value="2026-05">May 2026</option>
                <option value="2026-06">June 2026</option>
                <option value="2026-07">July 2026</option>
                <option value="2026-08">August 2026</option>
            </select>
        </div>
        
        <div class="tabs">
            <button class="tab active" onclick="switchTab('overview')">Overview</button>
            <button class="tab" onclick="switchTab('groceries')">Grocery Inventory</button>
            <button class="tab" onclick="switchTab('meals')">Meal Cost Calculator</button>
            <button class="tab" onclick="switchTab('expenses')">All Expenses</button>
        </div>
        
        <!-- OVERVIEW TAB -->
        <div id="overview" class="tab-content active">
            <div class="stats-grid">
                <div class="stat-card">
                    <div class="stat-value" id="totalSpent">€0.00</div>
                    <div class="stat-label">Total Spent This Month</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value" id="avgMealCost">€0.00</div>
                    <div class="stat-label">Average Meal Cost</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value" id="groceryValue">€0.00</div>
                    <div class="stat-label">Current Grocery Inventory Value</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value" id="dailyAvg">€0.00</div>
                    <div class="stat-label">Daily Average Spending</div>
                </div>
            </div>
        </div>
        
        <!-- GROCERY INVENTORY TAB -->
        <div id="groceries" class="tab-content">
            <div class="form-section">
                <h3>Add Grocery Item</h3>
                <div class="form-row">
                    <div class="input-group">
                        <label>Product Name</label>
                        <input type="text" id="productName" placeholder="e.g., Bread">
                    </div>
                    <div class="input-group">
                        <label>Total Price (€)</label>
                        <input type="number" id="productPrice" step="0.01" placeholder="2.50">
                    </div>
                    <div class="input-group">
                        <label>Total Quantity</label>
                        <input type="number" id="productQuantity" step="0.01" placeholder="500">
                    </div>
                    <div class="input-group">
                        <label>Unit</label>
                        <select id="productUnit">
                            <option value="g">grams (g)</option>
                            <option value="ml">milliliters (ml)</option>
                            <option value="pieces">pieces</option>
                            <option value="kg">kilograms (kg)</option>
                            <option value="l">liters (l)</option>
                        </select>
                    </div>
                </div>
                <button class="btn" onclick="addGroceryItem()">Add Item</button>
            </div>
            
            <div class="table-container">
                <table>
                    <thead>
                        <tr>
                            <th>Product</th>
                            <th>Total Price</th>
                            <th>Quantity</th>
                            <th>Unit</th>
                            <th>Price per Unit</th>
                            <th>Remaining</th>
                            <th>Value Left</th>
                            <th>Actions</th>
                        </tr>
                    </thead>
                    <tbody id="groceryTable">
                    </tbody>
                </table>
            </div>
        </div>
        
        <!-- MEAL CALCULATOR TAB -->
        <div id="meals" class="tab-content">
            <div class="form-section">
                <h3>Calculate Meal Cost</h3>
                <div class="form-row">
                    <div class="input-group">
                        <label>Meal Name</label>
                        <input type="text" id="mealName" placeholder="e.g., Breakfast, Lunch">
                    </div>
                </div>
                
                <h4 style="margin: 20px 0 15px 0; color: #2d3748;">Select Ingredients:</h4>
                <div id="ingredientSelector"></div>
                
                <div id="selectedIngredients"></div>
                
                <div class="meal-cost" id="mealCostDisplay" style="display: none;">
                    Total Meal Cost: €0.00
                </div>
                
                <button class="btn" onclick="saveMeal()" style="margin-top: 15px;">Save Meal</button>
            </div>
            
            <div class="table-container">
                <h3 style="margin-bottom: 15px; color: #2d3748;">Meal History</h3>
                <table>
                    <thead>
                        <tr>
                            <th>Date</th>
                            <th>Meal Name</th>
                            <th>Ingredients</th>
                            <th>Total Cost</th>
                            <th>Actions</th>
                        </tr>
                    </thead>
                    <tbody id="mealHistory">
                    </tbody>
                </table>
            </div>
        </div>
        
        <!-- ALL EXPENSES TAB -->
        <div id="expenses" class="tab-content">
            <div class="form-section">
                <h3>Add Other Expense</h3>
                <div class="form-row">
                    <div class="input-group">
                        <label>Description</label>
                        <input type="text" id="expenseDesc" placeholder="e.g., Transport, Utilities">
                    </div>
                    <div class="input-group">
                        <label>Amount (€)</label>
                        <input type="number" id="expenseAmount" step="0.01" placeholder="15.00">
                    </div>
                    <div class="input-group">
                        <label>Category</label>
                        <select id="expenseCategory">
                            <option value="Food">Food</option>
                            <option value="Transport">Transport</option>
                            <option value="Utilities">Utilities</option>
                            <option value="Entertainment">Entertainment</option>
                            <option value="Health">Health</option>
                            <option value="Other">Other</option>
                        </select>
                    </div>
                </div>
                <button class="btn" onclick="addExpense()">Add Expense</button>
            </div>
            
            <div class="table-container">
                <table>
                    <thead>
                        <tr>
                            <th>Date</th>
                            <th>Description</th>
                            <th>Category</th>
                            <th>Amount</th>
                            <th>Actions</th>
                        </tr>
                    </thead>
                    <tbody id="expenseTable">
                    </tbody>
                </table>
            </div>
        </div>
    </div>

    <script>
        // Data storage with localStorage persistence and monthly filtering
        let currentMonth = '2025-09'; // Default to September 2025
        let allGroceryItems = JSON.parse(localStorage.getItem('allGroceryItems') || '[]');
        let allMeals = JSON.parse(localStorage.getItem('allMeals') || '[]');
        let allExpenses = JSON.parse(localStorage.getItem('allExpenses') || '[]');
        let selectedIngredients = [];

        // Filtered data for current month
        let groceryItems = [];
        let meals = [];
        let expenses = [];

        // Save data to localStorage
        function saveData() {
            localStorage.setItem('allGroceryItems', JSON.stringify(allGroceryItems));
            localStorage.setItem('allMeals', JSON.stringify(allMeals));
            localStorage.setItem('allExpenses', JSON.stringify(allExpenses));
        }

        // Get current month string
        function getCurrentMonthString() {
            return currentMonth;
        }

        // Filter data by current month
        function filterDataByMonth() {
            groceryItems = allGroceryItems.filter(item => item.month === currentMonth);
            meals = allMeals.filter(meal => meal.month === currentMonth);
            expenses = allExpenses.filter(expense => expense.month === currentMonth);
        }

        // Change month functionality
        function changeMonth() {
            currentMonth = document.getElementById('monthSelector').value;
            filterDataByMonth();
            updateAllDisplays();
        }

        // Tab switching
        function switchTab(tabName) {
            document.querySelectorAll('.tab').forEach(tab => tab.classList.remove('active'));
            document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));
            
            event.target.classList.add('active');
            document.getElementById(tabName).classList.add('active');
            
            if (tabName === 'meals') {
                updateIngredientSelector();
            }
            if (tabName === 'overview') {
                updateOverview();
            }
        }

        // Grocery management
        function addGroceryItem() {
            const name = document.getElementById('productName').value;
            const price = parseFloat(document.getElementById('productPrice').value);
            const quantity = parseFloat(document.getElementById('productQuantity').value);
            const unit = document.getElementById('productUnit').value;
            
            if (!name || !price || !quantity) {
                alert('Please fill all fields');
                return;
            }
            
            const item = {
                id: Date.now(),
                name,
                totalPrice: price,
                totalQuantity: quantity,
                unit,
                pricePerUnit: price / quantity,
                remaining: quantity,
                dateAdded: new Date().toLocaleDateString(),
                month: currentMonth
            };
            
            allGroceryItems.push(item);
            groceryItems.push(item);
            saveData();
            
            // Clear form
            document.getElementById('productName').value = '';
            document.getElementById('productPrice').value = '';
            document.getElementById('productQuantity').value = '';
            
            updateGroceryTable();
            updateOverview();
        }

        function updateGroceryTable() {
            const tbody = document.getElementById('groceryTable');
            tbody.innerHTML = '';
            
            groceryItems.forEach(item => {
                const valueLeft = (item.remaining / item.totalQuantity) * item.totalPrice;
                const row = tbody.insertRow();
                row.innerHTML = `
                    <td>${item.name}</td>
                    <td>€${item.totalPrice.toFixed(2)}</td>
                    <td>${item.totalQuantity} ${item.unit}</td>
                    <td>${item.unit}</td>
                    <td>€${item.pricePerUnit.toFixed(4)}</td>
                    <td>${item.remaining.toFixed(2)} ${item.unit}</td>
                    <td>€${valueLeft.toFixed(2)}</td>
                    <td><button class="delete-btn" onclick="deleteGroceryItem(${item.id})">Delete</button></td>
                `;
            });
        }

        function deleteGroceryItem(id) {
            allGroceryItems = allGroceryItems.filter(item => item.id !== id);
            groceryItems = groceryItems.filter(item => item.id !== id);
            saveData();
            updateGroceryTable();
            updateOverview();
        }

        // Meal cost calculation
        function updateIngredientSelector() {
            const selector = document.getElementById('ingredientSelector');
            selector.innerHTML = '';
            
            if (groceryItems.length === 0) {
                selector.innerHTML = '<p style="color: #718096;">Add grocery items first to calculate meal costs</p>';
                return;
            }
            
            groceryItems.forEach(item => {
                if (item.remaining > 0) {
                    const div = document.createElement('div');
                    div.className = 'ingredient-item';
                    div.innerHTML = `
                        <span>${item.name} (${item.remaining.toFixed(2)} ${item.unit} available - €${item.pricePerUnit.toFixed(4)}/${item.unit})</span>
                        <button class="btn" onclick="addIngredientToMeal(${item.id})">Add to Meal</button>
                    `;
                    selector.appendChild(div);
                }
            });
        }

        function addIngredientToMeal(itemId) {
            const item = allGroceryItems.find(g => g.id === itemId);
            const quantity = prompt(`How much ${item.name} did you use? (in ${item.unit})`);
            
            if (!quantity || quantity <= 0) return;
            
            const usedQuantity = parseFloat(quantity);
            if (usedQuantity > item.remaining) {
                alert(`You only have ${item.remaining} ${item.unit} remaining!`);
                return;
            }
            
            const cost = usedQuantity * item.pricePerUnit;
            
            selectedIngredients.push({
                name: item.name,
                quantity: usedQuantity,
                unit: item.unit,
                cost: cost,
                itemId: itemId
            });
            
            updateSelectedIngredients();
            calculateMealCost();
        }

        function updateSelectedIngredients() {
            const container = document.getElementById('selectedIngredients');
            container.innerHTML = '<h4 style="margin: 15px 0; color: #2d3748;">Meal Ingredients:</h4>';
            
            selectedIngredients.forEach((ing, index) => {
                const div = document.createElement('div');
                div.className = 'ingredient-item';
                div.innerHTML = `
                    <span>${ing.name}: ${ing.quantity} ${ing.unit} - €${ing.cost.toFixed(3)}</span>
                    <button class="delete-btn" onclick="removeIngredient(${index})">Remove</button>
                `;
                container.appendChild(div);
            });
        }

        function removeIngredient(index) {
            selectedIngredients.splice(index, 1);
            updateSelectedIngredients();
            calculateMealCost();
        }

        function calculateMealCost() {
            const total = selectedIngredients.reduce((sum, ing) => sum + ing.cost, 0);
            const display = document.getElementById('mealCostDisplay');
            display.textContent = `Total Meal Cost: €${total.toFixed(3)}`;
            display.style.display = total > 0 ? 'block' : 'none';
        }

        function saveMeal() {
            const mealName = document.getElementById('mealName').value;
            if (!mealName || selectedIngredients.length === 0) {
                alert('Please enter meal name and add ingredients');
                return;
            }
            
            const totalCost = selectedIngredients.reduce((sum, ing) => sum + ing.cost, 0);
            
            // Update remaining quantities in grocery items
            selectedIngredients.forEach(ing => {
                const item = allGroceryItems.find(g => g.id === ing.itemId);
                if (item) {
                    item.remaining -= ing.quantity;
                }
            });
            
            const meal = {
                id: Date.now(),
                name: mealName,
                ingredients: [...selectedIngredients],
                totalCost: totalCost,
                date: new Date().toLocaleDateString(),
                month: currentMonth
            };
            
            allMeals.push(meal);
            meals.push(meal);
            saveData();
            
            // Clear form
            document.getElementById('mealName').value = '';
            selectedIngredients = [];
            updateSelectedIngredients();
            calculateMealCost();
            updateMealHistory();
            updateGroceryTable();
            updateOverview();
            
            alert(`Meal "${mealName}" saved! Cost: €${totalCost.toFixed(3)}`);
        }

        function updateMealHistory() {
            const tbody = document.getElementById('mealHistory');
            tbody.innerHTML = '';
            
            meals.slice().reverse().forEach(meal => {
                const row = tbody.insertRow();
                const ingredientsList = meal.ingredients.map(ing => 
                    `${ing.name} (${ing.quantity}${ing.unit})`
                ).join(', ');
                
                row.innerHTML = `
                    <td>${meal.date}</td>
                    <td>${meal.name}</td>
                    <td>${ingredientsList}</td>
                    <td>€${meal.totalCost.toFixed(3)}</td>
                    <td><button class="delete-btn" onclick="deleteMeal(${meal.id})">Delete</button></td>
                `;
            });
        }

        function deleteMeal(id) {
            allMeals = allMeals.filter(meal => meal.id !== id);
            meals = meals.filter(meal => meal.id !== id);
            saveData();
            updateMealHistory();
            updateOverview();
        }

        // Other expenses
        function addExpense() {
            const desc = document.getElementById('expenseDesc').value;
            const amount = parseFloat(document.getElementById('expenseAmount').value);
            const category = document.getElementById('expenseCategory').value;
            
            if (!desc || !amount) {
                alert('Please fill all fields');
                return;
            }
            
            const expense = {
                id: Date.now(),
                description: desc,
                amount: amount,
                category: category,
                date: new Date().toLocaleDateString(),
                month: currentMonth
            };
            
            allExpenses.push(expense);
            expenses.push(expense);
            saveData();
            
            // Clear form
            document.getElementById('expenseDesc').value = '';
            document.getElementById('expenseAmount').value = '';
            
            updateExpenseTable();
            updateOverview();
        }

        function updateExpenseTable() {
            const tbody = document.getElementById('expenseTable');
            tbody.innerHTML = '';
            
            expenses.slice().reverse().forEach(expense => {
                const row = tbody.insertRow();
                row.innerHTML = `
                    <td>${expense.date}</td>
                    <td>${expense.description}</td>
                    <td>${expense.category}</td>
                    <td>€${expense.amount.toFixed(2)}</td>
                    <td><button class="delete-btn" onclick="deleteExpense(${expense.id})">Delete</button></td>
                `;
            });
        }

        function deleteExpense(id) {
            allExpenses = allExpenses.filter(expense => expense.id !== id);
            expenses = expenses.filter(expense => expense.id !== id);
            saveData();
            updateExpenseTable();
            updateOverview();
        }

        // Update all displays
        function updateAllDisplays() {
            updateGroceryTable();
            updateMealHistory();
            updateExpenseTable();
            updateOverview();
            if (document.getElementById('meals').classList.contains('active')) {
                updateIngredientSelector();
            }
        }

        // Overview calculations
        function updateOverview() {
            const totalGroceries = groceryItems.reduce((sum, item) => sum + item.totalPrice, 0);
            const totalOtherExpenses = expenses.reduce((sum, exp) => sum + exp.amount, 0);
            const totalSpent = totalGroceries + totalOtherExpenses;
            
            const avgMealCost = meals.length > 0 ? 
                meals.reduce((sum, meal) => sum + meal.totalCost, 0) / meals.length : 0;
            
            const currentGroceryValue = groceryItems.reduce((sum, item) => 
                sum + ((item.remaining / item.totalQuantity) * item.totalPrice), 0);
            
            const dailyAvg = totalSpent / getDaysInCurrentMonth();
            
            document.getElementById('totalSpent').textContent = `€${totalSpent.toFixed(2)}`;
            document.getElementById('avgMealCost').textContent = `€${avgMealCost.toFixed(3)}`;
            document.getElementById('groceryValue').textContent = `€${currentGroceryValue.toFixed(2)}`;
            document.getElementById('dailyAvg').textContent = `€${dailyAvg.toFixed(2)}`;
        }

        // Get days in current month for accurate daily average
        function getDaysInCurrentMonth() {
            const [year, month] = currentMonth.split('-');
            return new Date(year, month, 0).getDate();
        }

        // Initialize - load saved data and update displays
        document.addEventListener('DOMContentLoaded', function() {
            // Set current month as default
            document.getElementById('monthSelector').value = currentMonth;
            filterDataByMonth();
            updateAllDisplays();
        });
        
        // Initial setup
        filterDataByMonth();
        updateOverview();
    </script>
</body>
</html>
