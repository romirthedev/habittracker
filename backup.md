<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Momentum - Habit Tracker</title>
  <style>
    :root {
      --primary: #6366f1;
      --primary-light: #818cf8;
      --primary-dark: #4f46e5;
      --success: #10b981;
      --warning: #f59e0b;
      --danger: #ef4444;
      --gray-50: #f9fafb;
      --gray-100: #f3f4f6;
      --gray-200: #e5e7eb;
      --gray-300: #d1d5db;
      --gray-400: #9ca3af;
      --gray-500: #6b7280;
      --gray-600: #4b5563;
      --gray-700: #374151;
      --gray-800: #1f2937;
      --gray-900: #111827;
      --radius: 8px;
    }
    
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    }
    
    body {
      background-color: var(--gray-50);
      color: var(--gray-800);
      line-height: 1.5;
    }
    
    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 0 1rem;
    }
    
    header {
      background-color: white;
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
      position: sticky;
      top: 0;
      z-index: 10;
    }
    
    nav {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 1rem 0;
    }
    
    .logo {
      display: flex;
      align-items: center;
      font-weight: 700;
      font-size: 1.5rem;
      color: var(--primary);
    }
    
    .logo svg {
      margin-right: 8px;
    }
    
    .nav-links {
      display: flex;
      gap: 2rem;
    }
    
    .nav-link {
      color: var(--gray-600);
      text-decoration: none;
      font-weight: 500;
      transition: color 0.2s;
    }
    
    .nav-link:hover {
      color: var(--primary);
    }
    
    .nav-link.active {
      color: var(--primary);
    }
    
    main {
      padding: 2rem 0;
    }
    
    .page-title {
      margin-bottom: 2rem;
      font-size: 2rem;
      font-weight: 700;
      color: var(--gray-900);
    }
    
    .card {
      background-color: white;
      border-radius: var(--radius);
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
      padding: 1.5rem;
      margin-bottom: 1.5rem;
    }
    
    .card-title {
      font-size: 1.25rem;
      font-weight: 600;
      margin-bottom: 1rem;
      color: var(--gray-900);
    }
    
    .habits-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
      gap: 1.5rem;
      margin-bottom: 2rem;
    }
    
    .habit-card {
      display: flex;
      flex-direction: column;
      background-color: white;
      border-radius: var(--radius);
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
      overflow: hidden;
      transition: transform 0.2s, box-shadow 0.2s;
    }
    
    .habit-card:hover {
      transform: translateY(-2px);
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    }
    
    .habit-header {
      padding: 1.25rem;
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
    }
    
    .habit-info {
      flex: 1;
    }
    
    .habit-name {
      font-weight: 600;
      font-size: 1.125rem;
      margin-bottom: 0.5rem;
    }
    
    .habit-streak {
      display: flex;
      align-items: center;
      font-size: 0.875rem;
      color: var(--gray-600);
    }
    
    .habit-streak svg {
      margin-right: 4px;
      color: var(--warning);
    }
    
    .habit-menu {
      background: none;
      border: none;
      cursor: pointer;
      color: var(--gray-400);
      transition: color 0.2s;
    }
    
    .habit-menu:hover {
      color: var(--gray-600);
    }
    
    .habit-calendar {
      padding: 0 1.25rem 1.25rem;
    }
    
    .calendar-grid {
      display: grid;
      grid-template-columns: repeat(7, 1fr);
      gap: 4px;
    }
    
    .calendar-day {
      aspect-ratio: 1;
      border-radius: 4px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 0.75rem;
      font-weight: 500;
      cursor: pointer;
      transition: transform 0.1s;
    }
    
    .calendar-day:hover {
      transform: scale(1.05);
    }
    
    .calendar-day.completed {
      background-color: var(--primary-light);
      color: white;
    }
    
    .calendar-day.today {
      border: 2px solid var(--primary);
      font-weight: 700;
    }
    
    .calendar-day.empty {
      background-color: var(--gray-100);
    }
    
    .habit-footer {
      padding: 1rem 1.25rem;
      border-top: 1px solid var(--gray-100);
      display: flex;
      justify-content: space-between;
    }
    
    .habit-stats {
      display: flex;
      gap: 1rem;
    }
    
    .habit-stat {
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    
    .stat-value {
      font-weight: 700;
      font-size: 1.125rem;
      color: var(--gray-900);
    }
    
    .stat-label {
      font-size: 0.75rem;
      color: var(--gray-500);
    }
    
    .check-button {
      display: flex;
      align-items: center;
      gap: 0.5rem;
      background-color: var(--primary);
      color: white;
      border: none;
      border-radius: var(--radius);
      padding: 0.5rem 1rem;
      font-weight: 500;
      cursor: pointer;
      transition: background-color 0.2s;
    }
    
    .check-button:hover {
      background-color: var(--primary-dark);
    }
    
    .check-button:disabled {
      background-color: var(--success);
      cursor: default;
    }
    
    .add-habit {
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 0.5rem;
      background-color: white;
      color: var(--primary);
      border: 2px dashed var(--gray-200);
      border-radius: var(--radius);
      padding: 2rem;
      font-weight: 500;
      cursor: pointer;
      transition: border-color 0.2s, color 0.2s;
      height: 100%;
    }
    
    .add-habit:hover {
      border-color: var(--primary-light);
      color: var(--primary-dark);
    }
    
    .recent-activity {
      margin-top: 2rem;
    }
    
    .activity-list {
      margin-top: 1rem;
    }
    
    .activity-item {
      display: flex;
      align-items: center;
      padding: 0.75rem 0;
      border-bottom: 1px solid var(--gray-100);
    }
    
    .activity-item:last-child {
      border-bottom: none;
    }
    
    .activity-icon {
      width: 32px;
      height: 32px;
      border-radius: 50%;
      background-color: var(--primary-light);
      display: flex;
      align-items: center;
      justify-content: center;
      margin-right: 1rem;
      color: white;
    }
    
    .activity-content {
      flex: 1;
    }
    
    .activity-title {
      font-weight: 500;
      margin-bottom: 0.25rem;
    }
    
    .activity-time {
      font-size: 0.75rem;
      color: var(--gray-500);
    }
    
    .charts-container {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 1.5rem;
    }
    
    .progress-chart {
      display: flex;
      align-items: center;
      justify-content: center;
      height: 200px;
    }
    
    .progress-chart-container {
      position: relative;
      width: 160px;
      height: 160px;
    }
    
    .progress-circle {
      transform: rotate(-90deg);
      transform-origin: 50% 50%;
    }
    
    .progress-background {
      fill: none;
      stroke: var(--gray-200);
      stroke-width: 12;
    }
    
    .progress-value {
      fill: none;
      stroke: var(--primary);
      stroke-width: 12;
      stroke-linecap: round;
      transition: stroke-dashoffset 0.5s ease;
    }
    
    .progress-text {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      text-align: center;
    }
    
    .progress-percentage {
      font-size: 2rem;
      font-weight: 700;
      color: var(--gray-900);
      line-height: 1;
    }
    
    .progress-label {
      font-size: 0.875rem;
      color: var(--gray-500);
      margin-top: 0.25rem;
    }
    
    @media (max-width: 768px) {
      .charts-container {
        grid-template-columns: 1fr;
      }
    }

    /* Animations */
    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }

    .fade-in {
      animation: fadeIn 0.5s ease-in-out;
    }

    @keyframes slideIn {
      from { transform: translateY(20px); opacity: 0; }
      to { transform: translateY(0); opacity: 1; }
    }

    .slide-in {
      animation: slideIn 0.4s ease-out;
    }

    /* Modal */
    .modal-backdrop {
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba(0, 0, 0, 0.5);
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 100;
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.2s;
    }

    .modal-backdrop.active {
      opacity: 1;
      pointer-events: all;
    }

    .modal {
      background-color: white;
      border-radius: var(--radius);
      width: 90%;
      max-width: 500px;
      padding: 1.5rem;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
      transform: translateY(20px);
      opacity: 0;
      transition: transform 0.3s, opacity 0.3s;
    }

    .modal-backdrop.active .modal {
      transform: translateY(0);
      opacity: 1;
    }

    .modal-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 1.5rem;
    }

    .modal-title {
      font-size: 1.25rem;
      font-weight: 600;
    }

    .modal-close {
      background: none;
      border: none;
      cursor: pointer;
      color: var(--gray-400);
      transition: color 0.2s;
    }

    .modal-close:hover {
      color: var(--gray-600);
    }

    .form-group {
      margin-bottom: 1.25rem;
    }

    .form-label {
      display: block;
      margin-bottom: 0.5rem;
      font-weight: 500;
      color: var(--gray-700);
    }

    .form-input {
      width: 100%;
      padding: 0.75rem;
      border: 1px solid var(--gray-300);
      border-radius: var(--radius);
      transition: border-color 0.2s;
      font-size: 1rem;
    }

    .form-input:focus {
      outline: none;
      border-color: var(--primary);
      box-shadow: 0 0 0 2px rgba(99, 102, 241, 0.1);
    }

    .form-select {
      width: 100%;
      padding: 0.75rem;
      border: 1px solid var(--gray-300);
      border-radius: var(--radius);
      transition: border-color 0.2s;
      font-size: 1rem;
      appearance: none;
      background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='16' height='16' fill='%236b7280' viewBox='0 0 16 16'%3E%3Cpath d='M4.646 6.646a.5.5 0 0 1 .708 0L8 9.293l2.646-2.647a.5.5 0 0 1 .708.708l-3 3a.5.5 0 0 1-.708 0l-3-3a.5.5 0 0 1 0-.708z'/%3E%3C/svg%3E");
      background-repeat: no-repeat;
      background-position: right 0.75rem center;
      background-size: 16px 12px;
    }

    .form-select:focus {
      outline: none;
      border-color: var(--primary);
      box-shadow: 0 0 0 2px rgba(99, 102, 241, 0.1);
    }

    .form-actions {
      display: flex;
      justify-content: flex-end;
      gap: 1rem;
      margin-top: 2rem;
    }

    .btn {
      padding: 0.75rem 1.5rem;
      border-radius: var(--radius);
      font-weight: 500;
      cursor: pointer;
      transition: background-color 0.2s, border-color 0.2s;
    }

    .btn-secondary {
      background-color: white;
      border: 1px solid var(--gray-300);
      color: var(--gray-700);
    }

    .btn-secondary:hover {
      background-color: var(--gray-50);
      border-color: var(--gray-400);
    }

    .btn-primary {
      background-color: var(--primary);
      border: 1px solid var(--primary);
      color: white;
    }

    .btn-primary:hover {
      background-color: var(--primary-dark);
      border-color: var(--primary-dark);
    }
  </style>
</head>
<body>
  <header>
    <div class="container">
      <nav>
        <a href="#" class="logo">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M12 2L2 7l10 5 10-5-10-5z"/>
            <path d="M2 17l10 5 10-5"/>
            <path d="M2 12l10 5 10-5"/>
          </svg>
          Momentum
        </a>
        <div class="nav-links">
          <a href="#" class="nav-link active">Dashboard</a>
          <a href="#" class="nav-link">Stats</a>
          <a href="#" class="nav-link">Settings</a>
        </div>
      </nav>
    </div>
  </header>
  
  <main class="container slide-in">
    <h1 class="page-title">My Habits</h1>
    
    <div class="habits-grid">
      <!-- Habit Card 1 -->
      <div class="habit-card fade-in">
        <div class="habit-header">
          <div class="habit-info">
            <h3 class="habit-name">Morning Meditation</h3>
            <div class="habit-streak">
              <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <path d="M13 2L3 14h9l-1 8 10-12h-9l1-8z"/>
              </svg>
              12 day streak
            </div>
          </div>
          <button class="habit-menu">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <circle cx="12" cy="12" r="1"/>
              <circle cx="12" cy="5" r="1"/>
              <circle cx="12" cy="19" r="1"/>
            </svg>
          </button>
        </div>
        <div class="habit-calendar">
          <div class="calendar-grid">
            <div class="calendar-day empty">26</div>
            <div class="calendar-day empty">27</div>
            <div class="calendar-day empty">28</div>
            <div class="calendar-day">1</div>
            <div class="calendar-day completed">2</div>
            <div class="calendar-day completed">3</div>
            <div class="calendar-day completed">4</div>
            <div class="calendar-day completed">5</div>
            <div class="calendar-day completed">6</div>
            <div class="calendar-day completed">7</div>
            <div class="calendar-day completed">8</div>
            <div class="calendar-day completed">9</div>
            <div class="calendar-day completed">10</div>
            <div class="calendar-day completed">11</div>
            <div class="calendar-day completed">12</div>
            <div class="calendar-day completed">13</div>
            <div class="calendar-day">14</div>
            <div class="calendar-day completed">15</div>
            <div class="calendar-day completed">16</div>
            <div class="calendar-day completed">17</div>
            <div class="calendar-day completed">18</div>
            <div class="calendar-day completed">19</div>
            <div class="calendar-day completed">20</div>
            <div class="calendar-day completed">21</div>
            <div class="calendar-day today">22</div>
            <div class="calendar-day">23</div>
            <div class="calendar-day">24</div>
            <div class="calendar-day">25</div>
          </div>
        </div>
        <div class="habit-footer">
          <div class="habit-stats">
            <div class="habit-stat">
              <span class="stat-value">87%</span>
              <span class="stat-label">Success</span>
            </div>
            <div class="habit-stat">
              <span class="stat-value">27</span>
              <span class="stat-label">Days</span>
            </div>
          </div>
          <button class="check-button" id="checkMeditation">
            <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <polyline points="20 6 9 17 4 12"/>
            </svg>
            Check
          </button>
        </div>
      </div>
      
      <!-- Habit Card 2 -->
      <div class="habit-card fade-in" style="animation-delay: 0.1s">
        <div class="habit-header">
          <div class="habit-info">
            <h3 class="habit-name">Read 30 Minutes</h3>
            <div class="habit-streak">
              <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <path d="M13 2L3 14h9l-1 8 10-12h-9l1-8z"/>
              </svg>
              8 day streak
            </div>
          </div>
          <button class="habit-menu">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <circle cx="12" cy="12" r="1"/>
              <circle cx="12" cy="5" r="1"/>
              <circle cx="12" cy="19" r="1"/>
            </svg>
          </button>
        </div>
        <div class="habit-calendar">
          <div class="calendar-grid">
            <div class="calendar-day empty">26</div>
            <div class="calendar-day empty">27</div>
            <div class="calendar-day empty">28</div>
            <div class="calendar-day">1</div>
            <div class="calendar-day">2</div>
            <div class="calendar-day completed">3</div>
            <div class="calendar-day completed">4</div>
            <div class="calendar-day completed">5</div>
            <div class="calendar-day completed">6</div>
            <div class="calendar-day completed">7</div>
            <div class="calendar-day completed">8</div>
            <div class="calendar-day completed">9</div>
            <div class="calendar-day completed">10</div>
            <div class="calendar-day">11</div>
            <div class="calendar-day completed">12</div>
            <div class="calendar-day completed">13</div>
            <div class="calendar-day completed">14</div>
            <div class="calendar-day completed">15</div>
            <div class="calendar-day completed">16</div>
            <div class="calendar-day completed">17</div>
            <div class="calendar-day completed">18</div>
            <div class="calendar-day completed">19</div>
            <div class="calendar-day completed">20</div>
            <div class="calendar-day completed">21</div>
            <div class="calendar-day today">22</div>
            <div class="calendar-day">23</div>
            <div class="calendar-day">24</div>
            <div class="calendar-day">25</div>
          </div>
        </div>
        <div class="habit-footer">
          <div class="habit-stats">
            <div class="habit-stat">
              <span class="stat-value">81%</span>
              <span class="stat-label">Success</span>
            </div>
            <div class="habit-stat">
              <span class="stat-value">19</span>
              <span class="stat-label">Days</span>
            </div>
          </div>
          <button class="check-button" id="checkReading">
            <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <polyline points="20 6 9 17 4 12"/>
            </svg>
            Check
          </button>
        </div>
      </div>
      
      <!-- Habit Card 3 -->
      <div class="habit-card fade-in" style="animation-delay: 0.2s">
        <div class="habit-header">
          <div class="habit-info">
            <h3 class="habit-name">Exercise</h3>
            <div class="habit-streak">
              <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <path d="M13 2L3 14h9l-1 8 10-12h-9l1-8z"/>
              </svg>
              3 day streak
            </div>
          </div>
          <button class="habit-menu">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <circle cx="12" cy="12" r="1"/>
              <circle cx="12" cy="5" r="1"/>
              <circle cx="12" cy="19" r="1"/>
            </svg>
          </button>
        </div>
        <div class="habit-calendar">
          <div class="calendar-grid">
            <div class="calendar-day empty">26</div>
            <div class="calendar-day empty">27</div>
            <div class="calendar-day empty">28</div>
            <div class="calendar-day">1</div>
            <div class="calendar-day">2</div>
            <div class="calendar-day completed">3</div>
            <div class="calendar-day">4</div>
            <div class="calendar-day">5</div>
            <div class="calendar-day completed">6</div>
            <div class="calendar-day">7</div>
            <div class="calendar-day completed">8</div>
            <div class="calendar-day">9</div>
            <div class="calendar-day completed">10</div>
            <div class="calendar-day">11</div>
            <div class="calendar-day completed">12</div>
            <div class="calendar-day">13</div>
            <div class="calendar-day completed">14</div>
            <div class="calendar-day">15</div>
            <div class="calendar-day completed">16</div>
            <div class="calendar-day">17</div>
            <div class="calendar-day completed">18</div>
            <div class="calendar-day completed">19</div>
            <div class="calendar-day completed">20</div>
            <div class="calendar-day completed">21</div>
            <div class="calendar-day today">22</div>
            <div class="calendar-day">23</div>
            <div class="calendar-day">24</div>
            <div class="calendar-day">25</div>
          </div>
        </div>
        <div class="habit-footer">
          <div class="habit-stats">
            <div class="habit-stat">
              <span class="stat-value">52%</span>
              <span class="stat-label">Success</span>
            </div>
            <div class="habit-stat">
              <span class="stat-value">13</span>
              <span class="stat-label">Days</span>
            </div>
          </div>
          <button class="check-button" id="checkExercise">
            <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <polyline points="20 6 9 17 4 12"/>
            </svg>
            Check
          </button>
        </div>
      </div>
      
      <!-- Add Habit Card -->
      <button class="add-habit fade-in" style="animation-delay: 0.3s" id="addHabitBtn">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <line x1="12" y1="5" x2="12" y2="19"/>
          <line x1="5" y1="12" x2="19" y2="12"/>
        </svg>
        Add Habit
      </button>
    </div>
    
    <div class="card recent-activity">
      <h2 class="card-title">Recent Activity</h2>
      <div class="activity-list">
        <div class="activity-item">
          <div class="activity-icon">
            <<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/>
              <polyline points="22 4 12 14.01 9 11.01"/>
            </svg>
          </div>
          <div class="activity-content">
            <div class="activity-title">Completed "Morning Meditation"</div>
            <div class="activity-time">Today, 7:15 AM</div>
          </div>
        </div>
        <div class="activity-item">
          <div class="activity-icon">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/>
              <polyline points="22 4 12 14.01 9 11.01"/>
            </svg>
          </div>
          <div class="activity-content">
            <div class="activity-title">Completed "Exercise"</div>
            <div class="activity-time">Yesterday, 6:30 PM</div>
          </div>
        </div>
        <div class="activity-item">
          <div class="activity-icon">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/>
              <polyline points="22 4 12 14.01 9 11.01"/>
            </svg>
          </div>
          <div class="activity-content">
            <div class="activity-title">Completed "Read 30 Minutes"</div>
            <div class="activity-time">Yesterday, 9:45 PM</div>
          </div>
        </div>
        <div class="activity-item">
          <div class="activity-icon" style="background-color: var(--primary);">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M12 5v14"/>
              <path d="M5 12h14"/>
            </svg>
          </div>
          <div class="activity-content">
            <div class="activity-title">Created new habit "Learn Spanish"</div>
            <div class="activity-time">2 days ago, 10:30 AM</div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="charts-container">
      <div class="card">
        <h2 class="card-title">Weekly Progress</h2>
        <div class="progress-chart">
          <div class="progress-chart-container">
            <svg width="160" height="160" class="progress-circle">
              <circle cx="80" cy="80" r="70" class="progress-background"/>
              <circle cx="80" cy="80" r="70" class="progress-value" stroke-dasharray="440" stroke-dashoffset="110"/>
            </svg>
            <div class="progress-text">
              <div class="progress-percentage">75%</div>
              <div class="progress-label">Completed</div>
            </div>
          </div>
        </div>
      </div>
      
      <div class="card">
        <h2 class="card-title">Monthly Goal</h2>
        <div class="progress-chart">
          <div class="progress-chart-container">
            <svg width="160" height="160" class="progress-circle">
              <circle cx="80" cy="80" r="70" class="progress-background"/>
              <circle cx="80" cy="80" r="70" class="progress-value" stroke-dasharray="440" stroke-dashoffset="176"/>
            </svg>
            <div class="progress-text">
              <div class="progress-percentage">60%</div>
              <div class="progress-label">Achieved</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
  
  <!-- Add Habit Modal -->
  <div class="modal-backdrop" id="addHabitModal">
    <div class="modal">
      <div class="modal-header">
        <h2 class="modal-title">Add New Habit</h2>
        <button class="modal-close" id="closeModal">
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <line x1="18" y1="6" x2="6" y2="18"/>
            <line x1="6" y1="6" x2="18" y2="18"/>
          </svg>
        </button>
      </div>
      <form id="habitForm">
        <div class="form-group">
          <label for="habitName" class="form-label">Habit Name</label>
          <input type="text" id="habitName" class="form-input" placeholder="e.g. Morning Run" required>
        </div>
        <div class="form-group">
          <label for="habitFrequency" class="form-label">Frequency</label>
          <select id="habitFrequency" class="form-select" required>
            <option value="daily">Daily</option>
            <option value="weekdays">Weekdays</option>
            <option value="weekends">Weekends</option>
            <option value="weekly">Weekly</option>
          </select>
        </div>
        <div class="form-group">
          <label for="habitTime" class="form-label">Reminder Time (Optional)</label>
          <input type="time" id="habitTime" class="form-input">
        </div>
        <div class="form-group">
          <label for="habitColor" class="form-label">Color</label>
          <select id="habitColor" class="form-select">
            <option value="primary">Blue</option>
            <option value="success">Green</option>
            <option value="warning">Yellow</option>
            <option value="danger">Red</option>
          </select>
        </div>
        <div class="form-actions">
          <button type="button" class="btn btn-secondary" id="cancelAddHabit">Cancel</button>
          <button type="submit" class="btn btn-primary">Create Habit</button>
        </div>
      </form>
    </div>
  </div>
  
  <script>
    // DOM Elements
    const addHabitBtn = document.getElementById('addHabitBtn');
    const addHabitModal = document.getElementById('addHabitModal');
    const closeModal = document.getElementById('closeModal');
    const cancelAddHabit = document.getElementById('cancelAddHabit');
    const habitForm = document.getElementById('habitForm');
    const checkButtons = document.querySelectorAll('.check-button');
    
    // Show modal
    addHabitBtn.addEventListener('click', () => {
      addHabitModal.classList.add('active');
    });
    
    // Hide modal
    const hideModal = () => {
      addHabitModal.classList.remove('active');
    };
    
    closeModal.addEventListener('click', hideModal);
    cancelAddHabit.addEventListener('click', hideModal);
    
    // Close modal when clicking outside
    addHabitModal.addEventListener('click', (e) => {
      if (e.target === addHabitModal) {
        hideModal();
      }
    });
    
    // Handle form submission
    habitForm.addEventListener('submit', (e) => {
      e.preventDefault();
      
      // Get form values
      const name = document.getElementById('habitName').value;
      const frequency = document.getElementById('habitFrequency').value;
      const time = document.getElementById('habitTime').value;
      const color = document.getElementById('habitColor').value;
      
      // Here you would typically save the habit to a database
      console.log('New habit:', { name, frequency, time, color });
      
      // Reset form and close modal
      habitForm.reset();
      hideModal();
      
      // Show a success message or update UI
      alert(`New habit "${name}" created successfully!`);
    });
    
    // Handle check buttons
    checkButtons.forEach(button => {
      button.addEventListener('click', () => {
        button.disabled = true;
        button.innerHTML = `
          <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <polyline points="20 6 9 17 4 12"/>
          </svg>
          Done!
        `;
      });
    });
    
    // For demo: Initialize check buttons based on today
    const todayButtons = document.querySelectorAll('#checkMeditation');
    todayButtons.forEach(button => {
      button.disabled = true;
      button.innerHTML = `
        <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <polyline points="20 6 9 17 4 12"/>
        </svg>
        Done!
      `;
    });
  </script>
</body>
</html>
