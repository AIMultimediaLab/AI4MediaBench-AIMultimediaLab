Detailed results provide a way to convey additional information from the scoring program to the frontend of a competition. This is achieved by creating a detailed_results.html file (or any .html file if multiple are present, it will choose the first one alphabetically) in the output folder. To enable detailed results, set enable_detailed_results to True in the competition settings using YAML or an editor.

## Key points about detailed results:

The detailed_results.html file is continuously monitored for changes and updated on the frontend every time the file changes, providing users with a real-time feed from the compute worker.

The HTML file has no limitations on its content and can be used to convey any desired information. It can be used for various purposes, such as:
- Plotting data using a Python library like Matplotlib or Seaborn.
- Visualizing the learning curve over time in a reinforcement learning challenge.
- Displaying the slope of a linear regression model.
- Showing the location of clusters in a classification challenge.
- Displaying any additional data about the submission file that cannot be summarized as a score.
- How to include figures in the detailed_results.html file:

Figures can be included directly inside the HTML code by converting them into bytes format.

Here is an example of how to include figures in Python:

```
# Path
input_dir = '/app/input'    # Input from the ingestion program
output_dir = '/app/output/' # To write the scores
reference_dir = os.path.join(input_dir, 'ref')  # Ground truth data
prediction_dir = os.path.join(input_dir, 'res') # Prediction made by the model
score_file = os.path.join(output_dir, 'scores.json')          # Scores
html_file = os.path.join(output_dir, 'detailed_results.html') # Detailed feedback

def write_file(file, content):
    """ Write content in the file.
    """
    with open(file, 'a', encoding="utf-8") as f:
        f.write(content)

def make_figure(scores):
    x = get_dataset_names()
    y = [scores[dataset] for dataset in x]
    fig, ax = plt.subplots()
    ax.plot(x, y, 'bo')
    ax.set_ylabel('accuracy')
    ax.set title('Submission results')
    return fig

def fig_to_b64(fig):
    buf = io.BytesIO()
    fig.savefig(buf, format='png')
    buf.seek(0)
    fig_b64 = base64.b64encode(buf.getvalue()).decode('ascii')
    return fig_b64

def main():
    # Initialize detailed results
    write_file(html_file, '<h1>Detailed results</h1>') # Create the file to give real-time feedback

    # ... compute the scores

    # Create a figure for detailed results
    figure = fig_to_b64(make_figure(scores))
    write_file(html_file, f'<img src="data:image/png;base64,{figure}">')
```
This Python script demonstrates how to generate figures and embed them into the detailed_results.html file. You can use this mechanism to visualize and present additional information within a AI4Media competition.
