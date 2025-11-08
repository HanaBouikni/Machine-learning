import numpy as np
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import mean_absolute_error
import matplotlib.pyplot as plt

# Training dataset
X_train = np.array([
    [0, 1],
    [1, 2],
    [2, 3],
    [3, 4],
    [5, 6],
    [0, 0],
    [4, 5]
])

y_train = np.array([0, 0, 1, 1, 1, 0, 1])  # 0 = normal, 1 = spam

# Q1: Plot the training data
plt.figure(figsize=(10, 6))
spam = X_train[y_train == 1]
normal = X_train[y_train == 0]

plt.scatter(normal[:, 0], normal[:, 1], c='blue', marker='o', s=100, label='Normal (0)', edgecolors='black')
plt.scatter(spam[:, 0], spam[:, 1], c='red', marker='s', s=100, label='Spam (1)', edgecolors='black')

# Plot the new email to classify
X_test = np.array([[2, 1]])
plt.scatter(X_test[:, 0], X_test[:, 1], c='green', marker='*', s=300, label='New Email', edgecolors='black')

plt.xlabel('Number of Links', fontsize=12)
plt.ylabel('Number of Spam Keywords', fontsize=12)
plt.title('Email Spam Detection - Training Data Visualization', fontsize=14, fontweight='bold')
plt.legend()
plt.grid(True, alpha=0.3)
plt.tight_layout()
plt.savefig('training_data_plot.png', dpi=300, bbox_inches='tight')
print("✓ Plot saved as 'training_data_plot.png'")
plt.show()

# New email to classify
y_true = np.array([1])  # Assume it is actually spam

print("\n" + "="*60)
print("Q2: Testing KNN for K = 1, 3, 5")
print("="*60)

# Test kNN for K = 1, 3, 5
for k in [1, 3, 5]:
    knn = KNeighborsClassifier(n_neighbors=k)
    knn.fit(X_train, y_train)
    
    y_pred = knn.predict(X_test)
    mae = mean_absolute_error(y_true, y_pred)
    
    prediction_label = "Spam" if y_pred[0] == 1 else "Normal"
    correctness = "✓ CORRECT" if y_pred[0] == y_true[0] else "✗ INCORRECT"
    
    print(f"\nK = {k}:")
    print(f"  Predicted = {y_pred[0]} ({prediction_label}) {correctness}")
    print(f"  MAE = {mae}")

print("\n" + "="*60)
print("Analysis Summary")
print("="*60)
print("New email features: [2 links, 1 spam keyword]")
print("True label: 1 (Spam)")